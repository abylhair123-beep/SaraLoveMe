




<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <title>Сара ответь на вопрос</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    * { box-sizing: border-box; }

    body {
      margin: 0;
      height: 100vh;
      overflow: hidden;
      display: flex;
      justify-content: center;
      align-items: center;
      background: linear-gradient(135deg, #ff9a9e, #fad0c4);
      font-family: Arial, Helvetica, sans-serif;
    }

    .card {
      background: #ffffff;
      padding: 40px 50px;
      border-radius: 20px;
      text-align: center;
      box-shadow: 0 20px 40px rgba(0,0,0,0.2);
      z-index: 10;
    }

    h1 {
      margin-bottom: 30px;
      font-size: 28px;
    }

    .buttons {
      position: relative;
      display: flex;
      justify-content: center;
      gap: 20px;
    }

    button {
      padding: 12px 28px;
      font-size: 18px;
      border: none;
      border-radius: 12px;
      cursor: pointer;
      transition: transform 0.2s ease;
    }

    #yes {
      background: #4CAF50;
      color: white;
    }

    #no {
      background: #f44336;
      color: white;
      position: absolute;
    }

    @keyframes floatUp {
      from {
        transform: translateY(0) scale(1);
        opacity: 1;
      }
      to {
        transform: translateY(-110vh) scale(1.6);
        opacity: 0;
      }
    }

    .heart {
      position: fixed;
      bottom: -30px;
      animation: floatUp 3.5s linear forwards;
      pointer-events: none;
    }

    .final-text {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 42px;
      color: white;
      opacity: 0;
      z-index: 20;
      transition: opacity 2s ease;
      text-align: center;
    }

    .final-text.show {
      opacity: 1;
    }
  </style>
</head>
<body>

  <div class="card" id="card">
    <h1>Любишь меня?</h1>
    <div class="buttons">
      <button id="yes">Да</button>
      <button id="no">Нет</button>
    </div>
  </div>

  <div class="final-text" id="finalText">Я тебя тоже люблю, жаным ❤️</div>

  <audio id="bgm" loop>
    <source src="rinat-gaysin-suyemin.mp3" type="audio/mpeg">
  </audio>

  <script>
    const yesBtn = document.getElementById('yes');
    const noBtn  = document.getElementById('no');
    const card   = document.getElementById('card');
    const bgm    = document.getElementById('bgm');
    const finalText = document.getElementById('finalText');

    noBtn.addEventListener('mouseenter', () => {
      const x = Math.random() * 200 - 100;
      const y = Math.random() * 100 - 50;
      noBtn.style.transform = `translate(${x}px, ${y}px)`;
    });

    function createHeart() {
      const heart = document.createElement('div');
      heart.className = 'heart';
      heart.textContent = '❤️';
      heart.style.left = Math.random() * window.innerWidth + 'px';
      heart.style.fontSize = 18 + Math.random() * 26 + 'px';
      document.body.appendChild(heart);
      setTimeout(() => heart.remove(), 4000);
    }

    let heartInterval;

    yesBtn.addEventListener('click', () => {
      document.body.style.background = 'linear-gradient(135deg, #ff758c, #ff7eb3)';
      card.style.display = 'none';

      bgm.play().catch(() => {});

      if (navigator.vibrate) {
        navigator.vibrate([200, 100, 200]);
      }

      heartInterval = setInterval(() => {
        for (let i = 0; i < 5; i++) createHeart();
      }, 300);

      finalText.classList.add('show');
    });
  </script>

</body>
</html>
