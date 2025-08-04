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
      <div class="question" onclick="toggleAnswer(0)">・是否有停車位、充電設施</div>
      <div class="answer">飯店提供住客免費汽車平面停車場於地下一樓（限高2.2米），您可於入住當日直接進入地下一樓停放再搭乘電梯至一樓櫃檯登記入住，因車位有限，無法預做保留。
若館內停車場停滿，您可自行停放至近飯店步行5分鐘的二個公有停車場，東大路橋下(入口在中央路)或府後停車場，飯店將會支付您的停車費(請於退房１１：００前於櫃檯索取停車時數抵用後再行取車)。謝謝您。
<br>★新春其週末尖峰時段，停車需求量大，如遇等待狀況，造成您的不便，敬請見諒。
<br>★本館停車場無附設充電設施。
</div>
    </div>
    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(1)"> ・早餐供應時間？</div>
      <div class="answer">6:30 ~ 10:00</div>
    </div>
  </div>

</div>
    </div>
    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(1)"> ・是否可提供嬰兒床、床圍。？</div>
      <div class="answer">飯店備有嬰兒床、床圍免費租用，如需預訂使用請注意以下事項：
<br>￭	因安全考慮，嬰兒床僅限1歲以下幼兒使用。一歲以上幼童建議在爸媽監護下使用床圍，且須入住前安裝。
<br>￭ 數量不多，請於訂房同時提前告知此需求。謝謝您！
<br>￭ 由於房型空間限制，精緻客房（標準雙人房），無法提供嬰兒床服務。
</div>
    </div>
  </div>
</div>
    </div>
    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(1)"> ・是否可嬰兒澡盆、奶瓶消毒鍋？</div>
      <div class="answer">本飯店備有嬰兒澡盆、奶瓶消毒鍋免費租用。但因數量不多，如有需要請事先預訂保留。謝謝您！</div>
    </div>
  </div>  
  </div>
    </div>
    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(1)"> ・關於入住時間、行李寄存？</div>
      <div class="answer">飯店入住時間為下午15：00後，退房為11：00前。
<br>如您提前抵達可於交誼廳等待至入住時間，另外入住前後都可以寄放行李於櫃檯。謝謝您！
</div>
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

