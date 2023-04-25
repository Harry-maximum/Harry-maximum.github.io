# Harry-maximum.github.io

<html>
<head>
    <title>计时器</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f2f2f2;
        }

        .container {
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
            background-color: #fff;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
        }

        h1 {
            text-align: center;
            margin: 0 0 20px;
            color: #333;
        }

        .timer {
            font-size: 4em;
            text-align: center;
            margin: 0 0 40px;
            color: #333;
        }

        .buttons {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 40px;
        }

        .button {
            width: 100px;
            height: 50px;
            border: none;
            border-radius: 5px;
            font-size: 1.2em;
            font-weight: bold;
            color: #fff;
            background-color: #888;
            cursor: pointer;
            transition: background-color 0.2s ease-in-out;
        }

        .button:hover {
            background-color: #555;
        }

        .record-list {
            padding: 0;
            margin: 0;
            list-style: none;
        }

        .record {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
            padding: 10px;
            border-radius: 5px;
            background-color: #eee;
            color: #333;
            font-size: 1.2em;
        }

        .record span {
            flex-grow: 1;
        }

        .record .time {
            margin-right: 20px;
        }

        .record .status {
            margin-right: 20px;
            font-weight: bold;
        }
    </style>
</head>
<body>
<div class="container">
    <h1>计时器</h1>
    <div class="timer">00:00:00.000</div>

    <div class="buttons">
        <button class="button" data-status="cold">Cold</button>
        <button class="button" data-status="little cold">Little Cold</button>
        <button class="button" data-status="no feeling">No Feeling</button>
        <button class="button" data-status="little hot">Little Hot</button>
        <button class="button" data-status="hot">Hot</button>
    </div>

    <ul class="record-list"></ul>
</div>

<script>
    const timer = document.querySelector('.timer');
    const buttons = document.querySelectorAll('.button');
    const recordList = document.querySelector('.record-list');
    let intervalId = null;
    let startTime = null;
    let records = [];

    buttons.forEach(button => {
        button.addEventListener('click', () => {
            if (!startTime) {
                startTimer();
            }

            const status = button.dataset.status;
            const time = getTime();

            const record = {
                time: time,
                status: status};
            records.push(record);
            const recordHtml = `<li class="record"><span class="time">${time}</span><span class="status">${status}</span></li>`;
            recordList.insertAdjacentHTML('beforeend', recordHtml);
        });
    });

    function startTimer() {
        startTime = new Date().getTime();

        intervalId = setInterval(() => {
            const currentTime = new Date().getTime();
            const timeElapsed = new Date(currentTime - startTime);
            const hours = timeElapsed.getUTCHours().toString().padStart(2, '0');
            const minutes = timeElapsed.getUTCMinutes().toString().padStart(2, '0');
            const seconds = timeElapsed.getUTCSeconds().toString().padStart(2, '0');
            const milliseconds = timeElapsed.getUTCMilliseconds().toString().padStart(3, '0');

            timer.textContent = `${hours}:${minutes}:${seconds}.${milliseconds}`;
        }, 1);
    }

    function getTime() {
        const currentTime = new Date().getTime();
        const timeElapsed = new Date(currentTime - startTime);
        const hours = timeElapsed.getUTCHours().toString().padStart(2, '0');
        const minutes = timeElapsed.getUTCMinutes().toString().padStart(2, '0');
        const seconds = timeElapsed.getUTCSeconds().toString().padStart(2, '0');
        const milliseconds = timeElapsed.getUTCMilliseconds().toString().padStart(3, '0');

        return `${hours}:${minutes}:${seconds}.${milliseconds}`;
    }
</script>
</body>
</html>
