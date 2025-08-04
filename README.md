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
      border-radius: 18px;
      padding: 30px 20px;
      width: 100%;
      max-width: 1200px;
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
      <div class="question" onclick="toggleAnswer(0)">1.是否有停車位、充電設施</div>
      <div class="answer">飯店提供住客免費汽車平面停車場於地下一樓（限高2.2米），您可於入住當日直接進入地下一樓停放再搭乘電梯至一樓櫃檯登記入住，因車位有限，無法預做保留。
若館內停車場停滿，您可自行停放至近飯店步行5分鐘的二個公有停車場，東大路橋下(入口在中央路)或府後停車場，飯店將會支付您的停車費(請於退房１１：００前於櫃檯索取停車時數抵用後再行取車)。謝謝您。
停車資訊：https://www.solhotel.com.tw/location/index.php?index_id=27
★新春其週末尖峰時段，停車需求量大，如遇等待狀況，造成您的不便，敬請見諒。
★本館停車場無附設充電設施。
</div>
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

