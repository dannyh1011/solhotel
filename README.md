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
      color: #FFC107;
      margin-bottom: 8px;
    }

    .answer {
      display: none;
      font-size: 1.2rem;
      color: #ffffff;
      padding-left: 15px;
      line-height: 1.6;
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
      <div class="question" onclick="toggleAnswer(0)">・是否有停車位、充電設施? </div>
      <div class="answer">飯店提供住客免費汽車平面停車場於地下一樓（限高2.2米），您可於入住當日直接進入地下一樓停放，再搭乘電梯至一樓櫃檯登記入住，因車位有限，無法預做保留。
        <br>若館內停車場停滿，您可自行停放至距離飯店步行5分鐘的二個公有停車場，東大路橋下(入口在中央路)或府後停車場，飯店將會支付您的停車費(請於退房11：00前於櫃檯索取停車時數抵用後再行取車)。謝謝您。
        <br>★新春及週末尖峰時段，停車需求量大，如遇等待車位狀況，造成您的不便，敬請見諒。
        <br>★本館停車場無附設充電設施。
      </div>
    </div>

    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(1)">・早餐內容、供應時間？</div>
      <div class="answer">歐式Buffet，提供中式、西式與日式餐 點。用餐時間6:30 ~ 10:00，核對房號及用餐人數即可用餐。遇年節尖峰用餐時間限時1小時。</div>
    </div>

    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(2)">・是否可提供嬰兒床、床圍？</div>
      <div class="answer">飯店備有嬰兒床、床圍免費租用，如需預訂使用請注意以下事項：
        <br>￭ 因安全考慮，嬰兒床僅限1歲以下幼兒使用。一歲以上幼童建議在爸媽監護下使用床圍，且須入住前安裝。
        <br>￭ 數量不多，請於訂房同時提前告知此需求。謝謝您！
        <br>￭ 由於房型空間限制，精緻客房（標準雙人房），無法提供嬰兒床服務。
      </div>
    </div>

 <div class="qa-item">
      <div class="question" onclick="toggleAnswer(3)">・是否可提供嬰兒澡盆、奶瓶消毒鍋？</div>
      <div class="answer">本飯店備有嬰兒澡盆、奶瓶消毒鍋免費租用。但因數量不多，如有需要請事先預訂保留。謝謝您！</div>
    </div>

    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(4)">・兒童入住加價方式？</div>
      <div class="answer">兒童收費方式採身高計算。
        <br>￭ 1歲以下的嬰兒，館內有提供嬰兒床(數量有限，需提前預訂)。
        <br>￭ 110公分以下免加收費用。
        <br>￭ 110～140公分幼童，加收費用為$220。
        <br>￭ 140公分以上比照成人，建議加床。加床含早餐費用為$880 (新春$1200元)，加床不含早餐費用為$550 (新春$1000元)。
      </div>
    </div>   

    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(5)">・成人入住加價方式？</div>
      <div class="answer">含早餐加床：
        <br>￭ 每人酌收新台幣880元 (新春$1200元)。
        <br>￭ 僅增加住宿人數，每人酌收新台幣500元(新春$800元)。
        <br><br>不含早餐加床：
        <br>￭ 每人酌收新台幣550元 (新春$1000元)。
        <br>￭ 僅增加住宿人數，每人酌收新台幣400元 (新春$500元)。
      </div>
    </div>

    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(6)">・平日價、假日價定義說明？</div>
      <div class="answer">平日: 星期日，星期一~星期五
        <br>假日: 星期六及特殊節日
      </div>
    </div>

    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(7)">・詢問大眾交通、步行、接駁服務？</div>
      <div class="answer">￭ 台鐵→迎曦大飯店
        <br>新竹火車站→步行約8分鐘→抵達迎曦飯店 (東門國小後門)
        <br><br>￭ 高鐵→迎曦大飯店
        <br>於新竹高鐵站(竹北.六家)下車→轉乘台鐵六家站→至新竹終點站→
        步行約8分鐘→抵達迎曦飯店 (東門國小後門)
        <br><br>￭ 飯店無免費接駁服務。
      </div>
    </div>

    <div class="qa-item">
      <div class="question" onclick="toggleAnswer(8)">・關於入住時間、行李寄存？</div>
      <div class="answer">飯店入住時間為下午15：00後，退房時間為翌日11：00前。
        <br>如您提前抵達可於交誼廳等待至入住時間，另外入住前後都可以寄放行李於櫃檯。謝謝您！
      </div>
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
