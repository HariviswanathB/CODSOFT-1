# ALARM CLOCK APP
# Aim:
To Build an alarm clock app that allows users to set and manage alarms .
# Code
# HTML
```
<!DOCTYPE html>
<html lang="en">

<head>
	<meta charset="UTF-8">
	<meta name="viewport"
		content="width=device-width, 
				initial-scale=1.0">
	<link rel="stylesheet" href="style.css">
	<title>Advanced Alarm Clock</title>
</head>

<body>
	<div class="clock">
		<h3>
			ALARM CLOCK
		</h3>
		<div class="time" id="time">
			00:00:00
		</div>
		<div class="input-row">
			<div class="input-field">
				<label for="alarmDate">
					Select Date:
				</label>
				<input type="date"
					id="alarmDate"
					class="alarm-input"
					min="">
			</div>
			<div class="input-field">
				<label for="alarmTime">
					Select Time:
				</label>
				<input type="time" id="alarmTime"
					class="alarm-input">
			</div>
			<button id="setAlarm">
				Set Alarm
			</button>
		</div>
		<div class="alarms" id="alarms">
		</div>
	</div>
	<script src="script.js"></script>
</body>

</html>
```
# CSS
```
body {
	font-family: Arial, sans-serif;
	background:
		linear-gradient(45deg, #0ddd29, #bae208);
	color: #fff;
	display: flex;
	justify-content: center;
	align-items: center;
	min-height: 100vh;
	margin: 0;
}

.clock {
	text-align: center;
	background-color: #fff;
	border-radius: 10px;
	box-shadow: 0 0 10px rgba(135, 6, 227, 0.2);
	padding: 20px;
	width: 300px;
}

h1 {
	font-size: 2rem;
	color: rgb(15, 231, 243);
}

h3 {
	font-size: 1.0rem;
	color: #f20fea;
}

.time {
	font-size: 2rem;
	margin: 20px 0;
	color: #f14506;
}

.input-row {
	display: flex;
	flex-direction: column;
	gap: 10px;
	align-items: center;
}

.input-field {
	display: flex;
	flex-direction: column;
	align-items: center;
}

input[type="date"],
input[type="time"] {
	padding: 10px;
	font-size: 1rem;
	border: 1px solid #ccc;
	border-radius: 5px;
	width: 100%;
	max-width: 200px;
}

.button-row {
	display: flex;
	gap: 10px;
	justify-content: center;
	align-items: center;
}

#setAlarm,
#updateTime {
	background-color: #007bff;
	color: #fff;
	border: none;
	padding: 10px 20px;
	border-radius: 5px;
	cursor: pointer;
	font-size: 1rem;
	transition: background-color 0.3s;
}

#setAlarm:hover,
#updateTime:hover {
	background-color: #0056b3;
}

.alarms {
	margin-top: 20px;
	text-align: left;
	color: #333;
}

.alarm {
	background-color: #f0f0f0;
	border: 1px solid #ccc;
	border-radius: 5px;
	padding: 10px;
	margin: 10px 0;
	display: flex;
	justify-content: space-between;
	align-items: center;
	animation: fadeIn 0.5s ease-in-out;
	font-size: 14px;
}

@keyframes fadeIn {
	from {
		opacity: 0;
	}

	to {
		opacity: 1;
	}
}
```
# JavaScript
```
let time = document.getElementById("time");
let dateInput = document.getElementById("alarmDate");
let tInput = document.getElementById("alarmTime");
let btn = document.getElementById("setAlarm");
let contan = document.getElementById("alarms");
let interVal;
let maxValue = 3;
let cnt = 0;
let almTimesArray = [];
function timeChangeFunction() {
	let curr = new Date();
	let hrs = curr.getHours();
	let min = String(curr.getMinutes()).padStart(2, "0");
	let sec = String(curr.getSeconds()).padStart(2, "0");
	let period = "AM";
	if (hrs >= 12) {
		period = "PM";
		if (hrs > 12) {
			hrs -= 12;
		}
	}
	hrs = String(hrs).padStart(2, "0");
	time.textContent = `${hrs}:${min}:${sec} ${period}`;
}
function alarmSetFunction() {
	let now = new Date();
	let selectedDate = new Date(dateInput.value + "T" + tInput.value);
	if (selectedDate <= now) {
		alert(`Invalid time. Please select 
	a future date and time.`);
		return;
	}
	if (almTimesArray.includes(selectedDate.toString())) {
		alert(`You cannot set multiple 
	alarms for the same time.`);
		return;
	}
	if (cnt < maxValue) {
		let timeUntilAlarm = selectedDate - now;
		let alarmDiv = document.createElement("div");
		alarmDiv.classList.add("alarm");
		alarmDiv.innerHTML = `
			<span>
			${selectedDate.toLocaleString()}
			</span>
			<button class="delete-alarm">
			Delete
			</button>
		`;
		alarmDiv
			.querySelector(".delete-alarm")
			.addEventListener("click", () => {
				alarmDiv.remove();
				cnt--;
				clearTimeout(interVal);
				const idx = almTimesArray.indexOf(selectedDate.toString());
				if (idx !== -1) {
					almTimesArray.splice(idx, 1);
				}
			});
		interVal = setTimeout(() => {
			alert("Time to wake up!");
			alarmDiv.remove();
			cnt--;
			const alarmIndex = almTimesArray.indexOf(selectedDate.toString());
			if (alarmIndex !== -1) {
				almTimesArray.splice(alarmIndex, 1);
			}
		}, timeUntilAlarm);
		contan.appendChild(alarmDiv);
		cnt++;
		almTimesArray.push(selectedDate.toString());
	} else {
		alert("You can only set a maximum of 3 alarms.");
	}
}
function showAlarmFunction() {
	let alarms = contan.querySelectorAll(".alarm");
	alarms.forEach((alarm) => {
		let deleteButton = alarm.querySelector(".delete-alarm");
		deleteButton.addEventListener("click", () => {
			alarmDiv.remove();
			cnt--;
			clearTimeout(interVal);
			const alarmIndex = almTimesArray.indexOf(selectedDate.toString());
			if (alarmIndex !== -1) {
				almTimesArray.splice(alarmIndex, 1);
			}
		});
	});
}
showAlarmFunction();
setInterval(timeChangeFunction, 1000);
btn.addEventListener("click", alarmSetFunction);
timeChangeFunction();
```
# Output:
![Screenshot 2024-04-02 203156](https://github.com/HariviswanathB/CODSOFT-1/assets/119103855/c90ae970-fc71-4349-bd67-781ef3bf491d)
