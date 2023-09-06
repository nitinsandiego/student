---
toc: false
comments: false
layout: post
title: Stock Analysis
description: This is my stock analysis application 
courses: {csp: {week: 3}}
type: tangibles
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stock Market Analysis Tool</title>
</head>
<body>
    <h1>Stock Market Analysis Tool</h1>

    <!-- Input field for stock symbol -->
    <label for="stockSymbol">Enter Stock Symbol:</label>
    <input type="text" id="stockSymbol" placeholder="Enter Stock Symbol">
    <button onclick="fetchStockData()">Fetch Data</button>

    <!-- Display stock data -->
    <div id="stockData">
        <!-- Stock data will be displayed here -->
    </div>

    <script>
        function fetchStockData() {
            const stockSymbol = document.getElementById("stockSymbol").value;
            const stockDataElement = document.getElementById("stockData");

            if (stockSymbol) {
                // Replace 'YOUR_API_KEY' with your Alpha Vantage API key
                const apiKey = 'ET3GOEQED7722VE';
                const apiUrl = `https://www.alphavantage.co/query?function=TIME_SERIES_INTRADAY&symbol=${stockSymbol}&interval=5min&apikey=${apiKey}`;

                // Clear previous data
                stockDataElement.innerHTML = '';

                fetch(apiUrl)
                    .then(response => response.json())
                    .then(data => {
                        const metaData = data['Meta Data'];
                        const timeSeries = data['Time Series (5min)'];

                        // Display stock information
                        const stockInfoElement = document.createElement("div");
                        stockInfoElement.innerHTML = `
                            <h2>${metaData['2. Symbol']}</h2>
                            <p>Updated at: ${metaData['3. Last Refreshed']}</p>
                        `;
                        stockDataElement.appendChild(stockInfoElement);

                        // Display recent stock prices
                        const pricesElement = document.createElement("div");
                        pricesElement.innerHTML = '<h3>Recent Prices:</h3>';

                        for (const time in timeSeries) {
                            const priceData = timeSeries[time];
                            pricesElement.innerHTML += `
                                <p>${time}: ${priceData['1. open']}</p>
                            `;
                        }

                        stockDataElement.appendChild(pricesElement);
                    })
                    .catch(error => {
                        console.error("Error fetching stock data:", error);
                    });
            }
        }
    </script>
</body>
</html>