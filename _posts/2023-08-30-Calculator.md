---
toc: true
comments: true
layout: post
title: Calculator
description: This is my calculator and it made using HTML and JavaScript.
courses: {csp: {week: 2}}
type: hacks
---

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Calculator</title>
<style>
  body {
    font-family: Arial, sans-serif;
  }
  .calculator {
    width: 200px;
    border: 1px solid #ccc;
    padding: 10px;
    text-align: center;
    margin: 0 auto;
  }
  input[type="text"] {
    width: 100%;
    margin-bottom: 10px;
    padding: 5px;
  }
  button {
    width: 48%;
    padding: 5px;
    margin: 2%;
    font-size: 16px;
  }
</style>
</head>
<body>
  <div class="calculator">
    <input type="text" id="display" readonly>
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
    const display = document.getElementById('display');

    function appendToDisplay(value) {
      display.value += value;
    }

    function clearDisplay() {
      display.value = '';
    }

    function calculate() {
      try {
        display.value = eval(display.value);
      } catch (error) {
        display.value = 'Error';
      }
    }
  </script>
</body>
</html>
