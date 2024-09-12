---
layout: post
title: Picture Reveal
description: Picture Reveal 
permalink: /picture_reveal
menu: nav/sprint_1.html
comments: true
---
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Puzzle Reveal with Guessing Game</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      height: 100vh;
      background-color: #f0f0f0;
    }

    .puzzle-container {
      display: grid;
      grid-template-columns: repeat(2, 150px);
      grid-template-rows: repeat(2, 150px);
      gap: 5px;
      margin-bottom: 20px;
    }

    .puzzle-piece {
      width: 150px;
      height: 150px;
      background-image: url('https://upload.wikimedia.org/wikipedia/commons/thumb/e/e7/Vincent_Willem_van_Gogh%2C_Dutch_-_Sunflowers_-_Google_Art_Project.jpg/1200px-Vincent_Willem_van_Gogh%2C_Dutch_-_Sunflowers_-_Google_Art_Project.jpg'); /* Replace with your image */
      background-size: 300px 300px;
      opacity: 0;
      transition: opacity 0.5s ease;
    }

    #piece1 {
      background-position: 0 0;
    }

    #piece2 {
      background-position: -150px 0;
    }

    #piece3 {
      background-position: 0 -150px;
    }

    #piece4 {
      background-position: -150px -150px;
    }

    .guess-section {
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .timer {
      font-size: 1.5em;
      margin-bottom: 10px;
    }

    .score {
      font-size: 1.2em;
      margin-top: 10px;
    }
  </style>
</head>
<body>

  <div class="puzzle-container">
    <div class="puzzle-piece" id="piece1"></div>
    <div class="puzzle-piece" id="piece2"></div>
    <div class="puzzle-piece" id="piece3"></div>
    <div class="puzzle-piece" id="piece4"></div>
  </div>

  <div class="guess-section">
    <div class="timer">Time: <span id="time">0</span> seconds</div>
    <input type="text" id="guessInput" placeholder="Guess the painting..." />
    <button id="submitGuess">Submit Guess</button>
    <div class="score" id="scoreDisplay">Score: 0</div>
  </div>

  <script>
    const pieces = document.querySelectorAll('.puzzle-piece');
    const timeDisplay = document.getElementById('time');
    const guessInput = document.getElementById('guessInput');
    const submitGuessButton = document.getElementById('submitGuess');
    const scoreDisplay = document.getElementById('scoreDisplay');

    const correctAnswer = "Sunflower"; // Set the correct answer here
    let startTime = Date.now();
    let timerInterval;
    let isGameFinished = false;

    // Start revealing pieces one by one
    function revealPieces() {
      pieces.forEach((piece, index) => {
        setTimeout(() => {
          piece.style.opacity = 1;
        }, index * 1000); // Reveal one every second
      });
    }

    // Timer function
    function startTimer() {
      timerInterval = setInterval(() => {
        const currentTime = Math.floor((Date.now() - startTime) / 1000);
        timeDisplay.textContent = currentTime;
      }, 1000);
    }

    // Stop the timer and calculate score based on time
    function stopTimer() {
      clearInterval(timerInterval);
    }

    // Calculate score based on time (less time means higher score)
    function calculateScore(timeTaken) {
      const baseScore = 100;
      const score = Math.max(baseScore - timeTaken * 2, 0); // 2 points deducted per second
      return score;
    }

    // Handle guess submission
    submitGuessButton.addEventListener('click', () => {
      if (isGameFinished) return; // Prevent further guesses once the game is finished

      const userGuess = guessInput.value.trim();
      const timeTaken = Math.floor((Date.now() - startTime) / 1000);

      if (userGuess.toLowerCase() === correctAnswer.toLowerCase()) {
        stopTimer();
        isGameFinished = true;
        const score = calculateScore(timeTaken);
        scoreDisplay.textContent = `Score: ${score}`;
        alert(`Correct! You guessed it in ${timeTaken} seconds!`);
      } else {
        alert('Incorrect guess. Try again!');
      }
    });

    // Start revealing puzzle pieces and the timer
    setTimeout(revealPieces, 500);
    startTimer();

  </script>

</body>
</html>
