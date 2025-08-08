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
      font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
      color: white;
    }

    .container {
      max-width: 600px;
      width: 90%;
    }

    .qa {
      background-color: #333;
      margin: 10px 0;
      border-radius: 8px;
      overflow: hidden;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.5);
    }

    .question {
      padding: 15px 20px;
      background-color: #444;
      cursor: pointer;
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 18px;
      font-weight: bold;
    }

    .answer {
      padding: 15px 20px;
      background-color: #555;
      display: none;
      font-size: 16px;
      line-height: 1.5;
    }

    .answer.open {
      display: block;
    }

    .arrow {
      margin-left: 10px;
      font-size: 18px;
    }

    .language-selector {
      position: absolute;
      top: 20px;
      right: 20px;
      z-index: 999;
    }

    .language-selector select {
      padding: 6px 12px;
      font-size: 14px;
      border-radius: 6px;
      border: none;
      background-color: #ffffff;
      font-weight: bold;
      color: #000;
    }
  </style>
</head>
<body>
  <!-- 語言選單 -->
  <div class="language-selector">
    <select onchange="changeLanguage(this.value)">
      <option value="zh">繁體中文</option>
      <option value="en">English</option>
      <option value="ja">日本語</option>
    </select>
  </div>

  <div class="container" id="qaContainer"></div>

  <script>
    const qaData = {
      zh: [
        { q: "請問是否可以寄放行李？", a: "可以的，入住當日的入住前與退房後都可於櫃檯寄放。" },
        { q: "請問早餐時間？", a: "早餐時間為 06:30 至 10:00。" },
        { q: "是否提供無線網路？", a: "全館皆提供免費無線網路（Wi-Fi）。" }
      ],
      en: [
        { q: "Can I store my luggage at the hotel?", a: "Yes, you may store your luggage at the front desk before check-in and after check-out on the same day." },
        { q: "What time is breakfast served?", a: "Breakfast is served from 6:30 AM to 10:00 AM." },
        { q: "Is Wi-Fi available?", a: "Free Wi-Fi is available throughout the entire hotel." }
      ],
      ja: [
        { q: "荷物を預けることはできますか？", a: "はい、ご到着日のチェックイン前およびチェックアウト後にフロントでお預かり可能です。" },
        { q: "朝食の時間を教えてください。", a: "朝食は午前6時30分から10時までご利用いただけます。" },
        { q: "Wi-Fiは利用できますか？", a: "館内全体で無料Wi-Fiをご利用いただけます。" }
      ]
    };

    function createQA(language = 'zh') {
      const container = document.getElementById("qaContainer");
      container.innerHTML = "";
      qaData[language].forEach((item, index) => {
        const qaDiv = document.createElement("div");
        qaDiv.className = "qa";

        const question = document.createElement("div");
        question.className = "question";
        question.innerHTML = `<span>${item.q}</span><span class="arrow">▼</span>`;
        question.onclick = () => toggleAnswer(index);

        const answer = document.createElement("div");
        answer.className = "answer";
        answer.innerHTML = `<p>${item.a}</p>`;

        qaDiv.appendChild(question);
        qaDiv.appendChild(answer);
        container.appendChild(qaDiv);
      });

      toggleAnswer(0); // 預設展開第一題
    }

    function toggleAnswer(index) {
      const answers = document.querySelectorAll('.answer');
      const arrows = document.querySelectorAll('.arrow');

      answers.forEach((answer, i) => {
        const arrow = arrows[i];
        const isOpen = answer.classList.contains('open');

        if (i === index) {
          if (!isOpen) {
            answer.classList.add('open');
            arrow.textContent = '▲';
            answer.scrollIntoView({ behavior: 'smooth', block: 'start' });
          } else {
            answer.classList.remove('open');
            arrow.textContent = '▼';
          }
        } else {
          answer.classList.remove('open');
          arrow.textContent = '▼';
        }
      });
    }

    function changeLanguage(lang) {
      createQA(lang);
    }

    document.addEventListener("DOMContentLoaded", () => {
      createQA('zh'); // 預設為繁體中文
    });
  </script>
</body>
</html>
