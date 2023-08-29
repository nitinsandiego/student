---
toc: true
comments: false
layout: post
title: Number Guessing Game
description: This is my number guessing game. This is part of my process of personalizing my Github page. 
type: tangibles
courses: {csp: {week: 1, categories: [4.A]}}
categories: [C1.4]
---
<div id="game-container">
  <h2>Guess the Number Game</h2>
  <p>Try to guess the secret number between 1 and 100!</p>
  <input type="number" id="user-input" placeholder="Enter your guess">
  <button id="submit-button">Submit Guess</button>
  <p id="message"></p>
</div>

<script>
  const secretNumber = Math.floor(Math.random() * 100) + 1;
  const userInput = document.getElementById('user-input');
  const submitButton = document.getElementById('submit-button');
  const message = document.getElementById('message');

  submitButton.addEventListener('click', () => {
    const userGuess = parseInt(userInput.value);
    
    if (isNaN(userGuess)) {
      message.textContent = "Please enter a valid number.";
    } else if (userGuess < secretNumber) {
      message.textContent = "Try a higher number!";
    } else if (userGuess > secretNumber) {
      message.textContent = "Try a lower number!";
    } else {
      message.textContent = `Congratulations! You guessed the number ${secretNumber}!`;
      submitButton.disabled = true;
    }
  });
</script>