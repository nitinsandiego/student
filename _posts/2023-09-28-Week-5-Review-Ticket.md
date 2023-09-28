---
layout: post
title: Week 5 Review Ticket
description: This is my Week 5 Review Ticket
type: tangibles
comments: True
courses: {'csp': {'week': 5}}
---

## HTML Basics
- HTML is based on beginning and closing tags `<tagname>content</tagname>`. Note the “/” on the ending or closing tag of the pair
- Paragraph is `<p></p>`
- Link is `<a href="https://www.w3schools.com/html/default.asp">Visit W3Schools HTML Page</a>`
- Image is `<img alt="describe image" src="link to image" width="100" height="200">`
- Bold text is `<strong>Bolded Text</strong>`
- Italics are- `<i>Italic Text</i>`
- Button is `<button>some button text</button>`

## Javascript Data Types
- Stirng Data: Strings are used to store text. Various functions are available for string manipulation.
- Number Data Type: Numbers are used to store numerical values. Operations and formatting that can be performed.
- Array Data Type: Arrays are lists used to store multiple values. Important points & functions.
- Object Data Type: Objects store data as key-value pairs. Points to conside.
 
 ## Using Javascript with HTML DOM
- Workspace Update: Always run git pull to stay updated.
- Referencing HTML Elements: Use document.getElementById("idTag") to reference elements. The .innerHTML attribute allows access and modification of the content within tags.
- Element Creation & Insertion: document.createElement(type) creates elements. .appendChild(element) adds elements into the HTML structure.
- Utilizing Functions: Functions are defined to execute specific tasks. They can take parameters and return values. Events, like button clicks, can trigger these functions.

## Basics of Javascript
- Embedding JavaScript: JavaScript can be embedded into markdown or Jupyter cells using <script></script> tags. In Jupyter, %%html magic command allows HTML and JavaScript embedding.
- Console Logging: console.log is used for printing messages to the console. Access the console in different browsers through their respective developer tools (in VSCode, use Help-Toggle Developer Tools).
- Data Storage & Types: Learn data abstraction, with JavaScript offering basic data types like string, number, and boolean. Declare variables using var variableName = value;.
- Data Access & Manipulation: Access and manipulate stored data by calling variable names. For strings, use operators like + for concatenation and == for comparison.
- Number Operations: Basic arithmetic operations and comparisons are available. Use == for value comparison, and === for type and value comparison.
- Conditional Statements: if-else statements allow conditional execution of code blocks. Combine with operators for dynamic comparisons and responses.

## Javascript Errors
- Segment 1: Alphabet List: Intended Behavior: Create a list of characters from the string contained in the variable alphabet.
- What I Changed: The for loop's condition should be i < alphabet.length to iterate over each character in alphabet. Instead of pushing i (which is a number), push alphabet[i] to add each character to alphabetList.
- Segment 2: Numbered Alphabet: Intended Behavior: Print the number and corresponding character in alphabet based on letterNumber.
- What I Changed: Adjusted the loop's condition and corrected the console.log statement.
- Segment 3: Odd Numbers: Intended Behavior: Print all odd numbers below 10.
- What I Changed: Adjust the initialization and incrementation of i to produce odd numbers.
- Challenge Segment: Cost Calculator
- Goal: Error-proof the code and implement a user input test.
- What to Do: Develop tests for user inputs and expected outputs. Gradually implement features to pass these tests. Iterate until the program functions as expected.