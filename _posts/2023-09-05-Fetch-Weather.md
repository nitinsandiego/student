---
toc: false
comments: false
layout: post
title: Weather Reporter
description: Input the city you want to know the weather of and my code will give the weather. 
courses: {csp: {week: 3}}
type: tangibles
---
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            background: linear-gradient(to bottom, #83a4d4, #b6fbff);
            height: 100vh;
            margin: 0;
            color: #333;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .weather-container {
            background: rgba(255, 255, 255, 0.8);
            padding: 25px 40px;
            border-radius: 8px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
            width: 100%;
            max-width: 500px;
        }

        button {
            margin-top: 20px;
            padding: 10px 20px;
            border: none;
            background: #007BFF;
            color: #fff;
            border-radius: 5px;
            cursor: pointer;
            transition: background 0.3s;
        }

        button:hover {
            background: #0056b3;
        }

        h2 {
            font-weight: 500;
        }

        p {
            font-size: 1.1em;
            margin: 5px 0;
        }

        #weather-data img {
            width: 50px;
            vertical-align: middle;
        }
    </style>
</head>

<body>
    <div class="weather-container">
        <label for="location">Enter a city:</label>
        <input type="text" id="location" placeholder="Enter a city" style="width: 100%; padding: 10px; margin-top: 10px; border-radius: 5px; border: 1px solid #ccc;">
        <button onclick="fetchWeather()">Get Weather</button>
        <div id="weather-data"></div>
    </div>

    <script>
        function getWeatherEmoji(description) {
            if (description.includes("rain")) return "☔️";
            if (description.includes("cloud")) return "☁️";
            if (description.includes("sun")) return "☀️";
            if (description.includes("snow")) return "❄️";
            return "🌤"; // default emoji
        }

        function fetchWeather() {
            const locationInput = document.getElementById("location");
            const location = locationInput.value.trim();

            if (!location) {
                alert("Please enter a city.");
                return;
            }

            const apiKey = "2f154dace08459a35fe9522ff7de936d";
            const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${location}&appid=${apiKey}`;

            fetch(apiUrl)
                .then(response => response.json())
                .then(data => {
                    if (data.sys) {
                        const weatherContainer = document.getElementById("weather-data");
                        const emoji = getWeatherEmoji(data.weather[0].description);
                        weatherContainer.innerHTML = `
                            <br>
                            <h2>Weather in ${data.name}, ${data.sys.country} ${emoji}</h2>
                            <p>Temperature: ${(((data.main.temp - 273.15) * (9 / 5)) + 32).toFixed(2)}°F</p>
                            <p>Description: ${data.weather[0].description}</p>
                            <p>Humidity: ${data.main.humidity}%</p>
                            <p>Wind Speed: ${data.wind.speed} m/s</p>
                        `;
                    } else {
                        console.error("Error fetching weather data: Country information not available.");
                    }
                })
                .catch(error => {
                    console.error("Error fetching weather data:", error);
                });
        }
    </script>
</body>

</html>