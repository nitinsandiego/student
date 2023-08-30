---
toc: true
comments: false
layout: post
title: Calculator
description: This is my calculator and it made using HTML and JavaScript.
courses: {csp: {week: 2}}
type: hacks
---

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Calculator</title>
<style>
  /* Styling for the calculator */
  body {
    font-family: Arial, sans-serif;
  }
  .calculator {
    width: 240px;
    border: 1px solid #ccc;
    padding: 10px;
    text-align: center;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 5px;
  }
  input[type="text"] {
    grid-column: span 4;
    margin-bottom: 10px;
    padding: 5px;
  }
  button {
    padding: 10px;
    font-size: 16px;
  }
</style>
</head>
<body>
  <div class="calculator">
    <!-- Display for the calculator -->
    <input type="text" id="display" readonly>

    <!-- Buttons for numbers and operations -->
    <!-- Each button calls a corresponding function on click -->
    <button onclick="appendToDisplay('7')">7</button>
    <button onclick="appendToDisplay('8')">8</button>
    <button onclick="appendToDisplay('9')">9</button>
    <button onclick="appendToDisplay('+')">+</button>
    <button onclick="appendToDisplay('4')">4</button>
    <button onclick="appendToDisplay('5')">5</button>
    <button onclick="appendToDisplay('6')">6</button>
    <button onclick="appendToDisplay('-')">-</button>
    <button onclick="appendToDisplay('1')">1</button>
    <button onclick="appendToDisplay('2')">2</button>
    <button onclick="appendToDisplay('3')">3</button>
    <button onclick="appendToDisplay('*')">*</button>
    <button onclick="appendToDisplay('0')">0</button>
    <button onclick="clearDisplay()">C</button>
    <button onclick="calculate()">=</button>
    <button onclick="appendToDisplay('/')">/</button>
  </div>

  <script>
    // Get a reference to the display element
    const display = document.getElementById('display');

    // Function to append a value to the display
    function appendToDisplay(value) {
      display.value += value;
    }

    // Function to clear the display
    function clearDisplay() {
      display.value = '';
    }

    // Function to perform the calculation
    function calculate() {
      try {
        // Use eval to evaluate the expression in the display
        display.value = eval(display.value);
      } catch (error) {
        // Display "Error" if an exception occurs during evaluation
        display.value = 'Error';
      }
    }
  </script>
</body>
</html>
