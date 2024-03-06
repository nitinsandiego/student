---
toc: true
comments: true
layout: post
title: Debugging Event
courses: { csp: {week: 25} }
type: tangibles
---

Start backend using Debugging
![alt text](</student/images/Screenshot 2024-03-05 at 9.26.48 AM.png>)

Set break point at the beginning of endpoint code. I set up a break point before the JSON data reponse was sent to the frontend.
![alt text](</student/images/Screenshot 2024-03-05 at 9.23.15 AM.png>)

Start in frontend with split screen loading source for an API fetch using GET. I stepped through the code to see how the data was being processed. In the first picture, I was able to see the houses data being fetched from the backend. In the second picture, I was able to see the data being processed and the data being sent to the frontend. Here, I could see the house data being displayed on the frontend.
![alt text](</student/images/Screenshot 2024-03-05 at 9.23.33 AM.png>)
![alt text](</student/images/Screenshot 2024-03-05 at 9.23.46 AM.png>)

Set break point on fetch, inside .then, inside .fetch In the first picture, I set up a break point right before the backend url was being fetched. The second break picture shows the response from the backend url. This picture shows all my house data, which inlcudes a pictue of the house, its price, square feet, number of bedrooms, number of bathrooms, and most importanly, the address of the house. In the third picture, the data is displayed and users can see all the house data displayed.
![alt text](</student/images/Screenshot 2024-03-06 at 10.24.53 AM.png>)
![alt text](</student/images/Screenshot 2024-03-06 at 10.27.12 AM.png>)
![alt text](</student/images/Screenshot 2024-03-06 at 10.34.43 AM.png>)

Run frontend, screen capture break at fetch while examining Body. These pictures show break points in the code that allow me to see the data being processed.
![alt text](</student/images/Screenshot 2024-03-06 at 10.24.53 AM.png>)
![alt text](</student/images/Screenshot 2024-03-06 at 10.27.12 AM.png>)

Press play on frontend, observe stop inside of backend. 
<video height="400" controls src="/student/videos/Screen Recording 2024-03-06 at 10.38.50 AM.mov" title="Press play on frontend, observe stop inside of backend. "></video>

Press step over on backend until you have obtained data from database, screen capture Python Object.<br>
![alt text](</student/images/Screenshot 2024-03-06 at 10.42.20 AM.png>)

Press play button to end backend debugging session.
<video height="400" controls src="/student/videos/Screen Recording 2024-03-06 at 10.44.08 AM.mov" title="Press play button to end backend debugging session."></video>

Return to frontend debug session and step in until you see data, screen capture capturing break point and Data.<br>
![alt text](</student/images/Screenshot 2024-03-06 at 10.34.43 AM.png>)
