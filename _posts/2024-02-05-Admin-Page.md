---
comments: false
layout: post
title: Admin Page
courses: { csp: {week: 21} }
permalink: /adminpage
type: hacks
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin Page</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f1f1f1;
            margin: 0;
            padding: 0;
        }
        .container {
            max-width: 800px;
            margin: 50px auto;
            padding: 20px;
            background-color: #000;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
            color: #fff;
            font-size: 36px;
            margin-bottom: 30px;
        }
        p {
            font-size: 18px;
            line-height: 1.6;
            margin-bottom: 20px;
            color: #fff;
        }
        .formula1-logo {
            display: block;
            margin: 0 auto;
            width: 200px;
            height: auto;
        }
    </style>
</head>
<body>
<div class="container">
    <h1>Welcome to the Admin Page</h1>
    <br>
    <img class="formula1-logo" src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/33/F1.svg/2560px-F1.svg.png" alt="Formula 1 Logo">
    <br>
    <p>This page is exclusively for admins. Only users with the "Admin" role can access this content.</p>
</div>

<script>
    function getCookie(name) {
    const value = `; ${document.cookie}`;
    const parts = value.split(`; ${name}=`);
    if (parts.length === 2) return parts.pop().split(';').shift();
    }

    const jwtToken = getCookie('jwt');
    console.log(getCookie('jwt'));
    console.log(document.cookie);

    if (jwtToken) {
        // Parse the JWT token to extract the payload
        const tokenParts = jwtToken.split('.');
        const payload = JSON.parse(atob(tokenParts[1]));

        // Check if the role is "Admin"
        if (payload.role === "Admin") {
            // User has the "Admin" role, they can access the admin page
            // You can add the content of your admin page here
        } else {
            // User does not have the "Admin" role, redirect to unauthorized page
            window.location.href = "{{site.baseurl}}/401";
        }
    } else {
        // Handle the case where the JWT token is not found in cookies
        window.location.href = "{{site.baseurl}}/login";
        // You may choose to redirect the user to the login page or handle the error differently
    }
</script>

</body>
</html>
