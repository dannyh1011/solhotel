<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>QA 自動回覆</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      width: 100%;
      height: 100%;
      background-color: #1a1616; /* 黑色背景 */
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .qa-container {
      background-color: #333;
      border: 6px solid #a67c52; /* 棕色邊框 */
      border-radius: 12px;
      padding: 30px 20px;
      width: 90%;
      max-width: 600px;
      box-sizing: border-box;
    }

    .qa-item {
      margin-bottom: 25px;
    }

    .question {
      cursor: pointer;
      font-size: 1.4rem;
      color: #FFC107;
      margin-bottom: 8px;
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

    @media (max-width: 480px) {
      .qa-container {
        padding: 20px 15px;
      }
      .question {
        font-size: 1.2rem;
      }
      .answer {
        font-size: 1rem;
      }
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
