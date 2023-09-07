---
toc: false
comments: false
layout: post
title: Music Recommendation
description: This is my music recommendation application
courses: {csp: {week: 3}}
type: tangibles
---
<html>
<head>
    <meta charset="utf-8">
</head>
<body>
    <!-- User input field -->
    <label for="userInput">Enter your favorite genre or artist:</label>
    <input type="text" id="userInput">
    <button onclick="getRecommendations()">Get Recommendations</button>
    <div id="recommendations">
        <!-- Recommendations will be displayed here -->
    </div>
    <script>
        const apiKey = 'a5d1284fa777bdb75371d65b7cee89ad';
        function getRecommendations() {
            const userInput = document.getElementById('userInput').value;
            const url = `https://ws.audioscrobbler.com/2.0/?method=artist.gettoptracks&artist=${userInput}&api_key=${apiKey}&format=json`;
            fetch(url)
                .then(response => {
                    if (!response.ok) {
                        throw new Error(`HTTP error! Status: ${response.status}`);
                    }
                    return response.json();
                })
                .then(data => {
                    if (data && data.toptracks && Array.isArray(data.toptracks.track)) {
                        const recommendations = data.toptracks.track;
                        displayRecommendations(recommendations);
                    } else {
                        console.error('Invalid API response:', data);
                        alert('Invalid API response. Please try again later.');
                    }
                })
                .catch(error => {
                    console.error('Error fetching data:', error);
                    alert('Error fetching data. Please try again later.');
                });
        }
        function displayRecommendations(recommendations) {
            const recommendationsContainer = document.getElementById('recommendations');
            recommendationsContainer.innerHTML = ''; // Clear previous recommendations
            if (recommendations.length === 0) {
                recommendationsContainer.textContent = 'No recommendations found.';
            } else {
                recommendations.forEach(track => {
                    const trackName = track.name;
                    const artistName = track.artist.name;
                    const trackElement = document.createElement('p');
                    trackElement.textContent = `${trackName} by ${artistName}`;
                    recommendationsContainer.appendChild(trackElement);
                });
            }
        }
    </script>
</body>
</html>
