<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>VENOM ENERGY MODE</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      padding: 0;
      overflow: hidden;
      height: 100vh;
      background: black;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }

    /* تأثير خلفية تفاعلية بلونين متداخلين (ميه أسود وأحمر) */
    .energy-bg {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: linear-gradient(45deg, rgba(255, 0, 0, 0.2), rgba(0, 0, 0, 0.2));
      background-size: 200% 200%;
      animation: gradientMove 10s linear infinite;
      z-index: 0;
    }

    @keyframes gradientMove {
      0% { background-position: 0% 50%; }
      100% { background-position: 100% 50%; }
    }

    /* خيوط العنكبوت المتحركة */
    .web-line {
      position: absolute;
      width: 2px;
      height: 80px;
      background: linear-gradient(to bottom, rgba(255,0,0,0.6), transparent);
      top: -100px;
      left: 50%;
      animation: dropWeb 4s linear infinite;
    }

    @keyframes dropWeb {
      0% { transform: translateY(0) rotate(0deg); }
      100% { transform: translateY(110vh) rotate(360deg); }
    }

    .smoke {
      position: absolute;
      width: 300px;
      height: 300px;
      top: -40px;
      left: -40px;
      background: radial-gradient(circle, rgba(255,255,255,0.08) 0%, transparent 70%);
      animation: smokeMove 6s linear infinite;
      z-index: 1;
      border-radius: 50%;
    }

    @keyframes smokeMove {
      0% { transform: scale(1) translateY(0px); opacity: 0.3; }
      50% { transform: scale(1.1) translateY(-15px); opacity: 0.5; }
      100% { transform: scale(1) translateY(0px); opacity: 0.3; }
    }

    .button-container {
      position: absolute;
      top: 48%;  /* تحديد مكان زر التسجيل تحت النص بقليل */
      z-index: 2;
    }

    .register-button {
      padding: 15px 60px;
      font-size: 20px;
      border: none;
      border-radius: 40px;
      background: linear-gradient(90deg, red, black, red);
      background-size: 200% 200%;
      animation: gradientMove 4s linear infinite;
      color: white;
      font-weight: bold;
      cursor: pointer;
      box-shadow: 0 0 15px red;
      transition: transform 0.3s;
    }

    .register-button:hover {
      transform: scale(1.1);
    }

    @keyframes gradientMove {
      0% { background-position: 0% 50%; }
      100% { background-position: 100% 50%; }
    }

    .message {
      display: none;
      margin-top: 30px; /* زيادة المسافة بين الزر والرسالة */
      padding: 15px;
      border-radius: 30px;
      background: white;
      color: black;
      font-size: 18px;
      font-weight: bold;
      z-index: 2;
      position: absolute;
      top: 60%;  /* تحديد مكان الرسالة أسفل الزر */
    }
  </style>
</head>
<body>

  <!-- الخلفية الديناميكية مع تحرك الجهاز -->
  <div class="energy-bg"></div>

  <!-- خيوط العنكبوت -->
  <div class="web-line" style="left: 10%; animation-delay: 0s;"></div>
  <div class="web-line" style="left: 50%; animation-delay: 2s;"></div>
  <div class="web-line" style="left: 80%; animation-delay: 1s;"></div>

  <!-- زر التسجيل فقط -->
  <div class="button-container">
    <button class="register-button" onclick="triggerEffect()">تسجيل</button>
  </div>

  <!-- الرسالة -->
  <div class="message" id="message-box">الموقع في حاله تحديث </div>

  <script>
    // إظهار الرسالة عند الضغط على الزر
    function triggerEffect() {
      const messageBox = document.getElementById('message-box');
      
      // إخفاء الرسالة قبل عرضها مرة أخرى
      messageBox.style.display = 'none';  // أولاً نخفيها

      // ثم نعرض الرسالة بعد مدة قصيرة
      setTimeout(() => {
        messageBox.style.display = 'block';
      }, 100);  // تأخير بسيط لإظهار الرسالة
    }

    // تحريك الخلفية بالجهاز بشكل دائم
    window.addEventListener('deviceorientation', function(event) {
      const x = event.gamma;
      const y = event.beta;
      const bg = document.querySelector('.energy-bg');

      const moveX = x ? x / 90 * 50 : 0;
      const moveY = y ? y / 90 * 50 : 0;

      bg.style.backgroundPosition = `${50 + moveX}% ${50 + moveY}%`;
    });
  </script>
</body>
</html>
