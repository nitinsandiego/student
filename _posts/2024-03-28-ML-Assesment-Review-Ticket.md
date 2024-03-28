---
title: ML Assesment Review Ticket
layout: post
type: tangibles
courses: { csp: { week: 28 } }
---

# ML Assesment Review Ticket

![alt text](</student/images/Screenshot 2024-03-28 at 8.50.59 AM.png>)
This picture show the first thing users see when they open the app. It is a simple and clean design that is easy to interact with

![alt text](</student/images/Screenshot 2024-03-28 at 8.53.23 AM.png>)
This picture shows the user input the number of bedrooms, number of bathroms, square feet, and rent estimate. This is the first step in the process of getting a price estimate.

![alt text](</student/images/Screenshot 2024-03-28 at 8.58.20 AM.png>)
This is the house I am basing my test values on. As you can see, the house has 5 bedrooms, 6 bathrooms, 5,182 square feet, and a rent estimate of $12397. The actual price estimate by Zillow is $3,823,000

![alt text](</student/images/Screenshot 2024-03-28 at 9.01.12 AM.png>)
This is the result of the test values. The model predicted that the price estimate for the house would be $3,780,872.00. This is very close to the actual price estimate of $3,823,000. This shows that the model is accurate and can be used to predict the price of a house based on the input values.

Backend code:
```python
from flask import Flask, request, jsonify
from flask import Blueprint
from flask_restful import Api, Resource
import seaborn as sns
import pandas as pd
from sklearn.metrics import accuracy_score
from sklearn.preprocessing import OneHotEncoder
from sklearn.linear_model import LogisticRegression
import numpy as np
import pandas as pd
import os
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn import metrics


class RecEngine:
    
    regressor = None

    def __init__(self):
        self.buildModel()
        
    def buildModel(self):
        basedir = os.path.abspath(os.path.dirname(__file__))

        # Specify the file path
        file_path = basedir + "/../static/data/RealEstateData.csv"

        data = pd.read_csv(file_path)
        data = data.dropna()
        #print(data)

        self.regressor = LinearRegression()
        X = data.drop(['price', 'address', 'city', 'state', 'zipcode', 'latitude', 'longitude', 'homeType', 'imgSrc', 'PriceEstimate'], axis=1)
        Y = data['price']
        
        X_Train, X_Test, Y_Train, Y_Test = train_test_split(X, Y, test_size=0.2, random_state=0)
        self.regressor.fit(X_Train, Y_Train)

        Y_Prediction = self.regressor.predict(X_Test)

        df = pd.DataFrame({'Actual ': Y_Test, 'Predicted': Y_Prediction})
        # print(df)

        mae = metrics.mean_absolute_error(Y_Test, Y_Prediction)
        r2 = metrics.r2_score(Y_Test, Y_Prediction)
        
        # print("The model performance for testing set")
        # print("-------------------------------------")
        # print('MAE is {}'.format(mae))
        # print('R2 score is {}'.format(r2))

    def predictPrice(self, bathrooms, bedrooms, livingArea, RentEstimate):
        predicion = self.regressor.predict([[bathrooms, bedrooms, livingArea, RentEstimate]])
        return predicion[0]


# Instantiate the RecEngine class
'''rec_engine = RecEngine()
print(rec_engine.predictPrice(6, 7, 5251, 24225))'''
```
API route code:
```python
 class _MLPriceModel(Resource):
        model = RecEngine()

        def get(self):
            bed = int(request.args.get("bed"))
            bath = int(request.args.get("bath"))
            area = int(request.args.get("area"))
            rentestimate = int(request.args.get("rent"))
            return int(self.model.predictPrice(bath, bed, area rentestimate))      
```

Frontend code: 
```html
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
```

Summary: The house price estimate model is accurate and can be used to predict the price of a house based on the input values. The model predicted that the price estimate for the house would be $3,780,872.00. This is very close to the actual price estimate of $3,823,000. This shows that the model is accurate and can be used to predict the price of a house based on the input values. Some things to keep in mind are that too acurate could be a problem because the model could be overfitting the data. Also, the model could be improved by adding more data and features to the model. Overall, the model is accurate and can be used to predict the price of a house based on the input values.
