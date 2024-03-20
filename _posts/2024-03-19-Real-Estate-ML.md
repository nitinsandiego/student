---
title: Real Estate ML
layout: post
permalink: /realEstate
type: hacks
courses: { csp: { week: 27 } }
---

<style>
    body {
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        margin: 0;
        padding: 0;
        background-color: #f9f9f9;
    }

    #container {
        text-align: center;
        padding: 50px;
    }

    h2 {
        color: white;
    }

    form {
        background-color: #fff;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }

    label {
        display: block;
        margin-bottom: 10px;
        font-weight: bold;
        color: black;
    }

    input[type="number"] {
        width: 100%;
        padding: 10px;
        margin-bottom: 20px;
        border: 1px solid #ccc;
        border-radius: 4px;
        box-sizing: border-box;
    }

    button {
        padding: 10px 20px;
        background-color: #007bff;
        color: #fff;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        transition: background-color 0.3s;
    }

    button:hover {
        background-color: #0056b3;
    }

    #result {
        margin-top: 20px;
        font-size: 18px;
        color: white; /* Change text color to black */
    }
</style>
<body>
<div id="container">
    <h2>SoCal Property Price Estimate Calculator</h2>
    <form id="priceEstimateForm">
        <label for="bedrooms">Number of Bedrooms:</label>
        <input type="number" id="bedrooms" name="bedrooms" min="1" required><br><br>
        <label for="bathrooms">Number of Bathrooms:</label>
        <input type="number" id="bathrooms" name="bathrooms" min="1" required><br><br>
        <label for="livingArea">Living Area (sqft):</label>
        <input type="number" id="livingArea" name="livingArea" min="1" required><br><br>
        <label for="rentEstimate">Rent Estimate:</label>
        <input type="number" id="rentEstimate" name="rentEstimate" min="1" required><br><br>
        <button type="submit">Calculate</button>
    </form>
    <div id="result"></div> <!-- Place the result inside the white container -->
</div>

<script>
    document.getElementById('priceEstimateForm').addEventListener('submit', function(event) {
        event.preventDefault();
        const formData = new FormData(event.target);
        
        const bedrooms = formData.get('bedrooms');
        const bathrooms = formData.get('bathrooms');
        const livingArea = formData.get('livingArea');
        const rentEstimate = formData.get('rentEstimate');

        const apiUrl = `http://127.0.0.1:8181/api/house/mlpricemodel?bed=${bedrooms}&bath=${bathrooms}&area=${livingArea}&rent=${rentEstimate}`;

        fetch(apiUrl)
            .then(response => response.json())
            .then(data => {
                const priceEstimate = data;
                const formattedPrice = new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(priceEstimate);
                document.getElementById('result').textContent = `Estimated Price: ${formattedPrice}`;
            })
            .catch(error => {
                console.error('Error:', error);
                document.getElementById('result').textContent = 'An error occurred. Please try again later.';
            });
    });
</script>
</body>