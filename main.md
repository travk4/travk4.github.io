<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Majestic RP — Проверка</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      font-family: Arial, sans-serif;
      background: #000;
      color: #fff;
      overflow: hidden;
    }

    video.background-video {
      position: fixed;
      top: 0;
      left: 0;
      min-width: 100%;
      min-height: 100%;
      object-fit: cover;
      z-index: -1;
    }

    .container {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100%;
      text-align: center;
      padding: 20px;
    }

    .ip-address {
      font-size: 1.2em;
      margin: 20px 0;
    }

    button {
      padding: 10px 20px;
      font-size: 1em;
      margin-top: 20px;
      cursor: pointer;
    }
  </style>
  <script src="https://www.google.com/recaptcha/api.js" async defer></script>
</head>
<body>

  <!-- Видео-фон -->
  <video autoplay muted loop class="background-video">
    <source src="https://majestic-rp.ru/video/intro-bg.mp4" type="video/mp4">
    Ваш браузер не поддерживает видео.
  </video>

  <div class="container">
    <h1>Добро пожаловать на Majestic RP</h1>
    <div class="ip-address" id="ip">Ваш IP: определяем...</div>

    <!-- Капча -->
    <div class="g-recaptcha" data-sitekey="6LegMmUrAAAAADqD9jsGKNPMsPe0k5QouYIczVAV"></div>

    <button onclick="submitCaptcha()">Продолжить</button>
  </div>

  <script>
    // Получение IP-адреса
    fetch('https://api.ipify.org?format=json')
      .then(res => res.json())
      .then(data => {
        document.getElementById('ip').textContent = 'Ваш IP: ' + data.ip;
      })
      .catch(() => {
        document.getElementById('ip').textContent = 'Не удалось определить IP';
      });

    // Обработка капчи
    function submitCaptcha() {
      const response = grecaptcha.getResponse();
      if (!response) {
        alert('Пожалуйста, подтвердите, что вы не робот.');
        return;
      }

      // Капча пройдена — редирект
      window.location.href = 'https://majestic-rp.ru/';
    }
  </script>
</body>
</html>
