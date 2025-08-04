<!DOCTYPE html>
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
      background-color: #1a1616;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .qa-container {
      background-color: #333;
      border: 6px solid #a67c52;
      border-radius: 18px;
      padding: 30px 20px;
      width: 100%;
      max-width: 1200px;
      box-sizing: border-box;
      overflow-y: auto;
      max-height: 100vh;
    }

    .qa-item {
      margin-bottom: 25px;
    }

    .question {
      cursor: pointer;
      font-size: 1.4rem;
      color: #a67c52;
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
      <div class="answer">飯店提供住客免費汽車平面停車場於地下一樓（限高2.2米）... ★本館停車場無附設充電設施。</div>
    </div>

    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(1)">・早餐供應時間？</div>
      <div class="answer">6:30 ~ 10:00</div>
    </div>

    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(2)">・是否可提供嬰兒床、床圍？</div>
      <div class="answer">飯店備有嬰兒床、床圍免費租用...精緻客房（標準雙人房）無法提供嬰兒床服務。</div>
    </div>

    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(3)">・兒童入住加價方式？</div>
      <div class="answer">兒童收費方式採身高計算...加床不含早餐費用為$550 (新春$1000元)。</div>
    </div>

    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(4)">・是否可提供嬰兒澡盆、奶瓶消毒鍋？</div>
      <div class="answer">本飯店備有嬰兒澡盆、奶瓶消毒鍋免費租用。但因數量不多，如有需要請事先預訂保留。謝謝您！</div>
    </div>

    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(5)">・成人入住加價方式？</div>
      <div class="answer">含早餐加床：每人酌收880元... 僅增加住宿人數每人酌收500元（新春800元）等。</div>
    </div>

    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(6)">・平日價、假日價定義說明？</div>
      <div class="answer">平日: 星期日~星期五；假日: 星期六及特殊節日</div>
    </div>

    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(7)">・詢問大眾交通、步行、接駁服務？</div>
      <div class="answer">♦ 台鐵→迎曦大飯店...飯店無免費接駁服務。</div>
    </div>

    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(8)">・關於入住時間、行李寄存？</div>
      <div class="answer">入住時間為15:00後、退房11:00前...入住前後皆可寄放行李。</div>
    </div>
  </div>

  <script>
    function toggleAnswer(index) {
      const answers = document.querySelectorAll('.answer');
      answers.forEach((ans, i) => {
        ans.style.display = (i === index && ans.style.display !== 'block') ? 'block' : 'none';
      });
    }
  </script>

</body>
</html>
