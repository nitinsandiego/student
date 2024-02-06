---
comments: True
layout: post
title: Delete
courses: {'csp': {'week': 20}}
type: hacks
permalink: /deleteUser
---
<!-- 
A simple HTML login form with a Login action when button is pressed.  

The form triggers the login_user function defined in the JavaScript below when the Login button is pressed.
-->

<style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }
        .container {
            width: 300px;
            margin: 100px auto;
            padding: 20px;
            background-color: #fff;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .container h2 {
            text-align: center;
            margin-bottom: 20px;
        }
        .container p {
            margin-bottom: 10px;
        }
        .container label {
            display: block;
            font-weight: bold;
        }
        .userInput {
            width: 100%;
            padding: 8px;
            margin-top: 5px;
            margin-bottom: 15px;
            border: 1px solid #ccc;
            border-radius: 3px;
            box-sizing: border-box;
        }
        .container button {
            width: 100%;
            padding: 10px;
            background-color: #007bff;
            color: #fff;
            border: none;
            border-radius: 3px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        .container button:hover {
            background-color: #0056b3;
        }
        h2 {
            text-align: center;
            color: black;
        }
        p {
            color: black;
        }
    </style>
<body>
    <div class="container">
        <h2>Delete User Form</h2>
        <form id="username" action="javascript:login_user()">
            <p><label for="uid">User ID:</label></p>
            <p><input class="userInput" type="text" name="uid" id="uid" required></p>
            <p><button onclick="login_user()">Delete</button></p>
        </form>
    </div>
</body>


<!-- 
Below JavaScript code is designed to handle user authentication in a web application. It's written to work with a backend server that uses JWT (JSON Web Tokens) for authentication.

The script defines a function when the page loads. This function is triggered when the Login button in the HTML form above is pressed. 
 -->
<script type="module">
    // uri variable and options object are obtained from config.js
    import { uri, options } from '{{site.baseurl}}/assets/js/api/config.js';
    localStorage.setItem('userID',document.getElementById("uid").value);
    const url = uri + '/api/users/authenticate';
    const body = {
            // name: document.getElementById("name").value,
            uid: "toby",
            password: "123toby"
            // dob: document.getElementById("dob").value
        };
    const authOptions = {
            ...options,// This will copy all properties from options
            method: 'POST', // Override the method property
            cache: 'no-cache', // Set the cache property
            body: JSON.stringify(body)
        };
    fetch(url, authOptions)

    function login_user(){
        // Set Authenticate endpoint
        const url = uri + '/api/users/';

        // Set the body of the request to include login data from the DOM
        const body = {
            // name: document.getElementById("name").value,
            uid: document.getElementById("uid").value,
            // dob: document.getElementById("dob").value
        };

        // Change options according to Authentication requirements
        const authOptions = {
            ...options, // This will copy all properties from options
            cache: 'no-cache',
            method: 'DELETE',
            body: JSON.stringify(body)
        };

        // Fetch JWT
        fetch(url, authOptions)
        .then(response => {
            // handle error response from Web API
            if (!response.ok) {
                const errorMsg = 'Login error: ' + response.status;
                console.log(errorMsg);
                return;
            }
            // Success!!!
            // Redirect to the database page
            window.location.href = "{{site.baseurl}}/lmc-login";
        })
        // catch fetch errors (ie ACCESS to server blocked)
        .catch(err => {
            console.error(err);
        });
    }

    // Attach login_user to the window object, allowing access to form action
    window.login_user = login_user;
</script>