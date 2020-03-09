# RPCCodes
<!DOCTYPE html>
<html>

<head>
	<title>RPC Countdown</title>
	<style>
		@import url('https://fonts.googleapis.com/css?family=Maven+Pro&display=swap');
		
		body {
			display: grid;
			justify-content: center;
		}
		
		#container {
			background: linear-gradient(to bottom right, #1f2023 50%, #1c1d20 50%);
			border-radius: 15px;
			border: 5px solid black;
			padding: 0.8% 2%;
			width: 400px;
			font-family: "Maven Pro", "Verdana", "Arial", sans-serif;
			text-align: center;
			font-weight: bold;
			font-size: 13px;
			color: #ddd;
		}

		#timer {
			display: grid;
			grid-auto-columns: repeat(4, 1fr);
			grid-auto-rows: 50px 15px;
			grid-column-gap: 10px;
			grid-row-gap: 10px;
			margin-top: 10px;
		}

		#timer-days {grid-column: 1 / 2;}
		#timer-hours {grid-column: 2 / 3;}
		#timer-minutes {grid-column: 3 / 4;}
		#timer-seconds {grid-column: 4 / 5;}

		#timer-days, #timer-hours, #timer-minutes, #timer-seconds {
			grid-row: 1;
			background-color: #151619;
			border: 3px solid #151619;
			border-radius: 10px;
			height: 50px;
			display: grid;
			align-items: center;
			font-style: normal;
			font-size: 35px;
			color: red;
		}

		.timer-label {
			grid-row: 2;
			font-style: normal;
			font-weight: bold;
			font-size: smaller;
		}
	</style>
	<script defer>
		function getUrlVars() {
			var vars = {};
			var parts = window.location.href.replace(/[?&]+([^=&]+)=([^&]*)/gi, function(m, key, value) {
				vars[key] = value;
			});
			return vars;
		}

		// Defining the target date

		rawTime = getUrlVars()["time"];

		// Setting up a loop to update the timer every second

		function updateTimer() {
			x = new Date();
			timeLeft = rawTime - x.getTime();

			if (timeLeft > 0) {
				secondsLeft = timeLeft / 1000;
				minutesLeft = secondsLeft / 60;
				hoursLeft = minutesLeft / 60;
				daysLeft = hoursLeft / 24;

				document.getElementById('timer-days').innerHTML = Math.floor(daysLeft);
				document.getElementById('timer-hours').innerHTML = Math.floor(hoursLeft % 24);
				document.getElementById('timer-minutes').innerHTML = Math.floor(minutesLeft % 60);
				document.getElementById('timer-seconds').innerHTML = Math.floor(secondsLeft % 60);
			} else {
				document.getElementById('label').innerHTML = '该条目可以删除。'
				document.getElementById('timer-days').innerHTML = '--'
				document.getElementById('timer-hours').innerHTML = '--'
				document.getElementById('timer-minutes').innerHTML = '--'
				document.getElementById('timer-seconds').innerHTML = '--'
				clearInterval(updateInterval);
			}
		}

		updateInterval = setInterval(updateTimer, 1000);
	</script>
</head>

<body>
	<div id="container">
		<img src="header2.png" width=200px align=center alt="RPC Authority" style="margin-bottom: 10px;"><br>
		<span id="label">该条目评分已到达删除线，将于</span>
		<div id="timer">
			<div id="timer-days"></div><div id="timer-hours"></div><div id="timer-minutes"></div><div id="timer-seconds"></div>
			<div class="timer-label" style="grid-column: 1 / 2">天</div>
			<div class="timer-label" style="grid-column: 2 / 3">小时</div>
			<div class="timer-label" style="grid-column: 3 / 4">分</div>
			<div class="timer-label" style="grid-column: 4 / 5">秒</div>
		</div>
    <span id="label">后删除。</span>
	</div>
</body>

</html>
