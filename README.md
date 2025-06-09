<!DOCTYPE html>
<html lang="en" >
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Moving Cookie Clicker Game</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background: #fff8dc;
      margin: 0;
      padding: 40px;
      overflow: hidden;
      position: relative;
      height: 100vh;
      user-select: none;
    }
    h1 {
      color: #d2691e;
    }
    #cookie {
      cursor: pointer;
      width: 100px;
      height: 100px;
      background: url('https://i.imgur.com/0M6pNqP.png') no-repeat center center;
      background-size: contain;
      position: absolute;
      top: 150px;
      left: 50%;
      transform: translateX(-50%);
      display: none;
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
      margin-top: 20px;
    }
    button:hover {
      background-color: #a0522d;
    }
  </style>
</head>
<body>

  <h1>Moving Cookie Clicker Game</h1>
  <div id="timer">Time left: 5s</div>
  <div id="score">Score: 0</div>

  <div id="cookie" title="Click me!"></div>

  <div id="message"></div>

  <button id="startBtn">Start Game</button>
  <button id="playAgainBtn" style="display:none;">Play Again</button>

<script>
  const cookie = document.getElementById('cookie');
  const scoreDisplay = document.getElementById('score');
  const timerDisplay = document.getElementById('timer');
  const message = document.getElementById('message');
  const startBtn = document.getElementById('startBtn');
  const playAgainBtn = document.getElementById('playAgainBtn');

  let score = 0;
  let timeLeft = 5;
  let gameActive = false;
  let timerInterval;

  function getRandomPosition() {
    // Get viewport width and height minus cookie size so it stays visible
    const cookieSize = 100;
    const padding = 20; // keep some padding from edges
    const maxX = window.innerWidth - cookieSize - padding;
    const maxY = window.innerHeight - cookieSize - padding;

    const x = Math.floor(Math.random() * maxX) + padding;
    const y = Math.floor(Math.random() * maxY) + padding;

    return { x, y };
  }

  function moveCookie() {
    const { x, y } = getRandomPosition();
    cookie.style.left = x + 'px';
    cookie.style.top = y + 'px';
  }

  function startGame() {
    score = 0;
    timeLeft = 5;
    gameActive = true;
    scoreDisplay.textContent = 'Score: 0';
    timerDisplay.textContent = `Time left: ${timeLeft}s`;
    message.textContent = '';
    cookie.style.display = 'block';
    startBtn.style.display = 'none';
    playAgainBtn.style.display = 'none';

    moveCookie();

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
    cookie.style.display = 'none';
    message.textContent = `Time's up! Your final score is ${score}.`;
    playAgainBtn.style.display = 'inline-block';
  }

  cookie.addEventListener('click', () => {
    if (!gameActive) return;
    score++;
    scoreDisplay.textContent = `Score: ${score}`;
    moveCookie();
  });

  startBtn.addEventListener('click', startGame);

  playAgainBtn.addEventListener('click', startGame);

</script>

</body>
</html>
