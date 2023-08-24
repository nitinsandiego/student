---
layout: default
title: Student Blog
---

# Nitin Balaji's Page

Go to my [Github account](https://github.com/nitinsandiego) !!

## About Me
Hi! This is Nitin Balaji. I am 15 years old. I am an aspiring coder and my dream job is to work as a software engineer. A little about is I am a huge fan of Formula 1 and my favorite F1 Team is Mercedes AMG Petronas Formual 1 Team, and my favorite driver is Lewis Hamilton. Not only am I avid Formula 1 fan, I am also a fan of NFL and my favorite NFL team is the Denver Broncos. Also, I am a sneaker head and love collecting shoes. I am really excited to be taking AP Computer Science Principles and also excited to take future software courses.

### My Interests
![MercedesAMGF1](images/MercedesAMGF1.jpg)
![LewisHamilton](images/LewisHamilton.png)
![DenverBroncos](images/DenverBroncos.png)
![Shoes](images/Shoes.png)

### My Favorite Youtube Channels
[Carwow](https://www.youtube.com/@carwow)
<iframe width="560" height="315" src="https://www.youtube.com/embed/TptzkkbC1vE?si=gL68VWEy3_62xeXS" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
<iframe width="560" height="315" src="https://www.youtube.com/embed/_FIVA-UhmZQ?si=ofKVulpE7yqUAo2j" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

[ThrottleHouse](https://www.youtube.com/@ThrottleHouse)
<iframe width="560" height="315" src="https://www.youtube.com/embed/7xf35zoQcC4?si=aaTvi1d6a1b25pYA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

[Doug Demuro](https://www.youtube.com/@DougDeMuro)
<iframe width="560" height="315" src="https://www.youtube.com/embed/kcmWknKtJkk?si=-aUZ7a7rKEBX7aiB" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## About Me Freeform Picture
My interests are coding, shoes, especially Jordans, Formula 1, and running.
![Freeform About Me](images/FreeformAboutMe.png)

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

## Calculator

<div id="calculator">
  <input type="text" id="calc-display" placeholder="0" readonly>
  <div id="buttons">
    <button onclick="appendNumber('7')">7</button>
    <button onclick="appendNumber('8')">8</button>
    <button onclick="appendNumber('9')">9</button>
    <button onclick="appendOperator('+')">+</button>
    <!-- Add more buttons for other numbers and operators -->
    <button onclick="calculate()">=</button>
    <button onclick="clearDisplay()">C</button>
  </div>
</div>

<script>
  let displayValue = '';

  function appendNumber(number) {
    displayValue += number;
    document.getElementById('calc-display').value = displayValue;
  }

  function appendOperator(operator) {
    displayValue += operator;
    document.getElementById('calc-display').value = displayValue;
  }

  function calculate() {
    try {
      displayValue = eval(displayValue);
      document.getElementById('calc-display').value = displayValue;
    } catch (error) {
      document.getElementById('calc-display').value = 'Error';
    }
  }

  function clearDisplay() {
    displayValue = '';
    document.getElementById('calc-display').value = displayValue;
  }
</script>


## Overview of Hacks, Study and Tangibles
Blogging in GitHub pages is a way to learn and code at the same time. 

- Plans, Lists, [Scrum Boards](https://clickup.com/blog/scrum-board/) help you to track key events, show progress and record time.  Effort is a big part of your class grade.  Show plans and time spent!
- [Hacks(Todo)](https://levelup.gitconnected.com/six-ultimate-daily-hacks-for-every-programmer-60f5f10feae) enable you to stay in focus with key requirements of the class.  Each Hack will produce Tangibles.
- Tangibles or [Tangible Artifacts](https://en.wikipedia.org/wiki/Artifact_(software_development)) are things you accumulate as a learner and coder. 


**Contact Info**
- Email: nitinsandiego@gmail.com
- School Email: nitinb07892@stu.powayusd.com
- Phone: (858)-312-9834
- Discord: lewishamilton4463