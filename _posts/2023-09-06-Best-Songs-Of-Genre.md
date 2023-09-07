---
toc: false
comments: false
layout: post
title: Best Songs by Music Genre
description: Input the genre you want and my code will give the best songs. 
courses: {csp: {week: 3}}
type: tangibles
---

<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Best Songs by Genre</title>
  <script>
    async function fetchBestSongs() {
      const genre = document.getElementById('genre').value; // Get genre from user input
      const apiKey = 'a5d1284fa777bdb75371d65b7cee89ad'; // Replace with your actual Last.fm API key
      const url = `http://ws.audioscrobbler.com/2.0/?method=tag.gettoptracks&tag=${genre}&api_key=${apiKey}&format=json`; // Construct API URL
      // Fetch data from Last.fm API
      const response = await fetch(url);
      const data = await response.json();
      // Clear the existing list
      document.getElementById('bestSongsList').innerHTML = '';
      // Populate the list with top tracks
      if(data.tracks && data.tracks.track) {
        data.tracks.track.forEach(track => {
          const listItem = document.createElement('li');
          listItem.textContent = `${track.name} by ${track.artist.name}`;
          document.getElementById('bestSongsList').appendChild(listItem);
        });
      } else {
        alert('No tracks found for this genre.');
      }
    }
  </script>
</head>
<body>
  <h1>Find the Best Songs by Genre</h1>
  
  <label for="genre">Enter Genre:</label>
  <input type="text" id="genre" name="genre">
  
  <button onclick="fetchBestSongs()">Find Best Songs</button>

  <h2>Best Songs:</h2>
  <ul id="bestSongsList">
    <!-- List items will be populated here -->
  </ul>
</body>
</html>
