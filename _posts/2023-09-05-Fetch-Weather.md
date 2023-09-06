---
toc: false
comments: false
layout: post
title: Weather Reporter
description: Input the city you want to know the weather of and my code will give the weather. 
courses: {csp: {week: 3}}
type: tangibles
---

<html>
<head>
    <title>Weather App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .weather-container {
            max-width: 400px;
            margin: 0 auto;
            padding: 20px;
            border: 1px solid #ccc;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
    </style>
</head>
<body>
    <h1>Weather App</h1>

<div class="weather-container">
        <label for="location">Enter a city:</label>
        <input type="text" id="location" placeholder="Enter a city">
        <button onclick="fetchWeather()">Get Weather</button>

        <div id="weather-data">
            <!-- Weather data will be displayed here -->
        </div>
</div>

<script>
        function fetchWeather() {
            var locationInput = document.getElementById("location");
            var location = locationInput.value.trim();

            if (location === "") {
                alert("Please enter a city.");
                return;
            }

            var apiKey = "2f154dace08459a35fe9522ff7de936d"; // Replace with your actual API key

            // Construct the API URL
            var apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${location}&appid=${apiKey}`;

            // Make the API request using the fetch function
            fetch(apiUrl)
        .then(response => response.json())
        .then(data => {
            // Check if the 'sys' object exists in the response
            if (data.sys) {
                var weatherContainer = document.getElementById("weather-data");
                weatherContainer.innerHTML = `
                    <br>
                    <h2>Weather in ${data.name}, ${data.sys.country}</h2>
                    <p>Temperature: ${(data.main.temp - 273.15).toFixed(2)}°C</p>
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
