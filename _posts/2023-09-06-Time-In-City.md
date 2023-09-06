---
toc: false
comments: false
layout: post
title: Time in City
description: Input the city you want to know the time of and my code will give the time. 
courses: {csp: {week: 3}}
type: tangibles
---
<html>
<head>
    <title>City Time</title>
</head>
<body>
    <h1>City Time</h1>
    <p>Enter a city name to get its current time:</p>
    <input type="text" id="cityInput" placeholder="Enter a city name">
    <button onclick="getCityTime()">Get Time</button>
    <p id="timeResult"></p>
    <script>
        function getCityTime() {
            const cityInput = document.getElementById('cityInput').value;
            const date = new Date();
            // Create a new Date object using UTC time to avoid time zone issues
            const utcDate = new Date(date.toUTCString());
            try {
                // Use the toLocaleTimeString function with the timeZone option to get the city's time
                const cityTime = utcDate.toLocaleTimeString([], { timeZone: cityInput, hour: '2-digit', minute: '2-digit', second: '2-digit' });
                document.getElementById('timeResult').textContent = `Current time in ${cityInput}: ${cityTime}`;
            } catch (error) {
                document.getElementById('timeResult').textContent = `Invalid time zone: ${cityInput}`;
            }
        }
    </script>
</body>
</html>
