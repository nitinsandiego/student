---
toc: false
comments: false
layout: post
title: Formula 1 Quiz
courses: {csp: {week: 2}}
type: tangibles
---

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Formula 1 Quiz</title>
<style>
  body {
    font-family: Arial, sans-serif;
  }
  #quiz-container {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }
  h2 {
    margin-top: 0;
  }
  label {
    display: block;
    margin-bottom: 10px;
    font-weight: bold;
  }
  input[type="radio"] {
    margin-right: 5px;
  }
  #submit-button {
    margin-top: 15px;
  }
</style>
</head>
<body>
<div id="quiz-container">
  <h2>Formula 1 Quiz</h2>
  <form id="quiz-form">
    <div class="question">
      <p>1. Who holds the record for the most Formula 1 World Championships?</p>
      <label><input type="radio" name="q1" value="a"> Ayrton Senna</label>
      <label><input type="radio" name="q1" value="b"> Lewis Hamilton</label>
      <label><input type="radio" name="q1" value="c"> Michael Schumacher</label>
    </div>
    <div class="question">
      <p>2. Which circuit is known for its iconic Eau Rouge corner?</p>
      <label><input type="radio" name="q2" value="a"> Monza</label>
      <label><input type="radio" name="q2" value="b"> Spa-Francorchamps</label>
      <label><input type="radio" name="q2" value="c"> Silverstone</label>
    </div>
    <div class="question">
      <p>3. Which team has won the most Constructors' Championships?</p>
      <label><input type="radio" name="q3" value="a"> Ferrari</label>
      <label><input type="radio" name="q3" value="b"> Mercedes</label>
      <label><input type="radio" name="q3" value="c"> Red Bull Racing</label>
    </div>
    <div class="question">
      <p>4. What is the official tire supplier for Formula 1?</p>
      <label><input type="radio" name="q4" value="a"> Bridgestone</label>
      <label><input type="radio" name="q4" value="b"> Pirelli</label>
      <label><input type="radio" name="q4" value="c"> Michelin</label>
    </div>
    <div class="question">
      <p>5. Which driver is known as the "Flying Finn"?</p>
      <label><input type="radio" name="q5" value="a"> Kimi Räikkönen</label>
      <label><input type="radio" name="q5" value="b"> Mika Häkkinen</label>
      <label><input type="radio" name="q5" value="c"> Valtteri Bottas</label>
    </div>
    <div class="question">
      <p>6. In which year did Formula 1 introduce hybrid power units?</p>
      <label><input type="radio" name="q6" value="a"> 2005</label>
      <label><input type="radio" name="q6" value="b"> 2014</label>
      <label><input type="radio" name="q6" value="c"> 2009</label>
    </div>
    <div id="submit-button">
      <button type="button" onclick="submitQuiz()">Submit Answers</button>
    </div>
  </form>
  <div id="results"></div>
</div>

<script>
function submitQuiz() {
  const answers = {
    q1: document.querySelector('input[name="q1"]:checked'),
    q2: document.querySelector('input[name="q2"]:checked'),
    q3: document.querySelector('input[name="q3"]:checked'),
    q4: document.querySelector('input[name="q4"]:checked'),
    q5: document.querySelector('input[name="q5"]:checked'),
    q6: document.querySelector('input[name="q6"]:checked')
    // Add more answers here...
  };

  const correctAnswers = {
    q1: 'b',
    q2: 'b',
    q3: 'a',
    q4: 'b',
    q5: 'a',
    q6: 'b'
    // Add more correct answers here...
  };

  let score = 0;

  for (const question in answers) {
    if (answers[question] && answers[question].value === correctAnswers[question]) {
      score++;
    }
  }

  const resultsContainer = document.getElementById('results');
  resultsContainer.innerHTML = `You scored ${score} out of ${Object.keys(correctAnswers).length}!`;
}
</script>
</body>
</html>
