<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>QA 自動回覆</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background-color: #1a1616;
      color: white;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    .qa-container {
      background-color: #333;
      border: 5px solid #a67c52;
      border-radius: 12px;
      padding: 30px 40px;
      width: 90%;
      max-width: 600px;
    }

    .qa-item {
      margin-bottom: 20px;
    }

    .question {
      cursor: pointer;
      font-size: 1.5rem;
      margin-bottom: 5px;
      color: #FFC107;
    }

    .answer {
      display: none;
      font-size: 1.2rem;
      color: #ffffff;
      padding-left: 15px;
    }

    .question:hover {
      text-decoration: underline;
    }
  </style>
</head>
<body>

  <div class="qa-container">
    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(0)">1. 請問是否可以寄放行李？</div>
      <div class="answer">可以的</div>
    </div>
    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(1)">2. 請問早餐時間？</div>
      <div class="answer">6:30 ~ 10:00</div>
    </div>
  </div>

  <script>
    function toggleAnswer(index) {
      const answers = document.querySelectorAll('.answer');
      const answer = answers[index];
      answer.style.display = (answer.style.display === 'block') ? 'none' : 'block';
    }
  </script>

</body>
</html>
