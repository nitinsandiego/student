---
toc: false
comments: false
layout: post
title: Image of Request
description: Input the image you want to see and my code will give the image. 
courses: {csp: {week: 3}}
type: tangibles
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Search</title>
</head>
<body>
    <h1>Image Search</h1>

    <!-- Input field for search query -->
    <label for="searchQuery">Search for an image:</label>
    <input type="text" id="searchQuery" placeholder="Enter your search query">
    <button onclick="searchImages()">Search</button>

    <!-- Display the search results -->
    <div id="imageResults">
        <!-- Images will be displayed here -->
    </div>

    <script>
        function searchImages() {
            const searchQuery = document.getElementById("searchQuery").value;
            const imageResults = document.getElementById("imageResults");

            if (searchQuery) {
                // Replace 'YOUR_ACCESS_KEY' with your actual Unsplash API access key
                const accessKey = 'jPfgEAqcNH-rY3xiVPMyoCjUyI84C92UFVfpXoopoGA';
                const apiUrl = `https://api.unsplash.com/search/photos?query=${searchQuery}&client_id=${accessKey}`;

                // Clear previous search results
                imageResults.innerHTML = '';

                fetch(apiUrl)
                    .then(response => response.json())
                    .then(data => {
                        const photos = data.results;
                        photos.forEach(photo => {
                            const imgElement = document.createElement("img");
                            imgElement.src = photo.urls.small;
                            imgElement.alt = photo.alt_description;
                            imageResults.appendChild(imgElement);
                        });
                    })
                    .catch(error => {
                        console.error("Error fetching images:", error);
                    });
            }
        }
    </script>
</body>
</html>