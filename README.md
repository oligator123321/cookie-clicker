<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Cookie Clicker Game</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background: #fff8dc;
      padding: 40px;
      margin: 0;
    }
    h1 {
      color: #d2691e;
    }
    #cookie {
      cursor: pointer;
      width: 150px;
      height: 150px;
      background: url('https://i.imgur.com/0M6pNqP.png') no-repeat center center;
      background-size: contain;
      margin: 20px auto;
      user-select: none;
    }
    #score, #timer {
      font-size: 1.5em;
      margin: 10px 0;
      color: #8b4513;
    }
    #message {
      font-size: 1.8em;
      margin: 30px 0;
      color: #a0522d;
    }
    button {
      padding: 10px 25px;
      font-size: 1.2em;
      background-color: #d2691e;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      display: none;
      margin-top: 20px;
    }
    button:hover {
      background-color: #a0522d;
    }
  </style>
</head>
<body>

  <h1>Cookie Clicker Game</h1>
  <div id="timer">Time left: 5s</div>
  <div id="score">Score: 0</div>

  <div id="cookie" title="Click me!"></div>

  <div id="message"></div>

  <button id="playAgainBtn">Play Again</button>

  <script>
    const cookie = document.getElementById('cookie');
    const scoreDisplay = document.getElementById('score');
    const timerDisplay = document.getElementById('timer');
    const message = document.getElementById('message');
    const playAgainBtn = document.getElementById('playAgainBtn');

    let score = 0;
    let timeLeft = 5;
    let gameActive = false;
    let timerInterval;

    function startGame() {
      score = 0;
      timeLeft = 5;
      gameActive = true;
      scoreDisplay.textContent = 'Score: 0';
      timerDisplay.textContent = `Time left: ${timeLeft}s`;
      message.textContent = '';
      playAgainBtn.style.display = 'none';

      timerInterval = setInterval(() => {
        timeLeft--;
        timerDisplay.textContent = `Time left: ${timeLeft}s`;
        if (timeLeft <= 0) {
          endGame();
        }
      }, 1000);
    }

    function endGame() {
      gameActive = false;
      clearInterval(timerInterval);
      message.textContent = `Time's up! Your final score is ${score}.`;
      playAgainBtn.style.display = 'inline-block';
    }

    cookie.addEventListener('click', () => {
      if (!gameActive) return;
      score++;
      scoreDisplay.textContent = `Score: ${score}`;
    });

    playAgainBtn.addEventListener('click', () => {
      startGame();
    });

    // Start the game immediately on page load
    startGame();
  </script>

</body>
</html>
