<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>QA 自動回覆</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      width: 100%;
      height: 100%;
      background-color: #1a1616;
      display: flex;
      flex-direction: column;
      justify-content: flex-start;
      align-items: center;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    .lang-switcher {
      margin: 20px;
    }

    .lang-switcher button {
      margin: 0 10px;
      padding: 8px 16px;
      font-size: 1rem;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      background-color: #a67c52;
      color: white;
      transition: background 0.3s;
    }

    .lang-switcher button:hover {
      background-color: #8b653f;
    }

    .qa-container {
      background-color: #2c2c2c;
      border: 6px solid #a67c52;
      border-radius: 20px;
      padding: 30px 25px;
      width: 90%;
      max-width: 1000px;
      box-sizing: border-box;
      overflow-y: auto;
      max-height: 90vh;
    }

    .qa-item {
      margin-bottom: 20px;
    }

    .question {
      cursor: pointer;
      font-size: 1.5rem;
      color: #FFC107;
      margin-bottom: 8px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      background-color: #444;
      padding: 12px 16px;
      border-radius: 10px;
      transition: background 0.3s;
    }

    .question:hover {
      background-color: #555;
    }

    .arrow {
      font-size: 1.2rem;
      color: #FFC107;
    }

    .answer {
      max-height: 0;
      overflow: hidden;
      transition: max-height 0.4s ease, padding 0.3s ease;
      font-size: 1.1rem;
      color: #ffffff;
      padding-left: 20px;
      line-height: 1.6;
      background-color: #3a3a3a;
      border-radius: 8px;
      padding: 0 16px;
    }

    .answer.open {
      max-height: 800px;
      padding: 15px 16px;
    }

    a {
      color: #00d4ff;
      text-decoration: underline;
    }

    @media (max-width: 600px) {
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
  <div class="lang-switcher">
    <button onclick="switchLang('zh')">中文</button>
    <button onclick="switchLang('en')">English</button>
    <button onclick="switchLang('ja')">日本語</button>
  </div>

  <div class="qa-container" id="qa">
    <!-- QA 將由 JS 注入 -->
  </div>

  <script>
    const qaData = {
      zh: [
        {
          q: "推薦景點1？",
          a: `巨城購物中心：<a href="https://maps.app.goo.gl/ZGFdxkC6ZZBUWAV96" target="_blank">點我查看地圖</a>`
        },
        {
          q: "推薦景點2？",
          a: `城隍廟：<a href="https://maps.app.goo.gl/JHym4kpXUj7L4cXr9" target="_blank">點我查看地圖</a>`
        }
      ],
      en: [
        {
          q: "Recommended Spot 1?",
          a: `Big City Shopping Mall: <a href="https://maps.app.goo.gl/ZGFdxkC6ZZBUWAV96" target="_blank">View on Google Maps</a>`
        },
        {
          q: "Recommended Spot 2?",
          a: `Chenghuang Temple: <a href="https://maps.app.goo.gl/JHym4kpXUj7L4cXr9" target="_blank">View on Google Maps</a>`
        }
      ],
      ja: [
        {
          q: "おすすめスポット1は？",
          a: `ビッグシティモール：<a href="https://maps.app.goo.gl/ZGFdxkC6ZZBUWAV96" target="_blank">Googleマップで見る</a>`
        },
        {
          q: "おすすめスポット2は？",
          a: `城隍廟：<a href="https://maps.app.goo.gl/JHym4kpXUj7L4cXr9" target="_blank">Googleマップで見る</a>`
        }
      ]
    };

    const container = document.getElementById('qa');

    function renderQA(lang) {
      container.innerHTML = '';
      qaData[lang].forEach((item, index) => {
        const qaItem = document.createElement('div');
        qaItem.className = 'qa-item';

        const question = document.createElement('div');
        question.className = 'question';
        question.innerHTML = `・${item.q} <span class="arrow">▼</span>`;
        question.onclick = () => toggleAnswer(index);

        const answer = document.createElement('div');
        answer.className = 'answer';
        answer.innerHTML = item.a;

        qaItem.appendChild(question);
        qaItem.appendChild(answer);
        container.appendChild(qaItem);
      });

      toggleAnswer(0); // 預設展開第一個
    }

    function toggleAnswer(index) {
      const answers = document.querySelectorAll('.answer');
      const arrows = document.querySelectorAll('.arrow');
      const answer = answers[index];
      const arrow = arrows[index];
      const isOpen = answer.classList.contains('open');

      answer.classList.toggle('open');
      arrow.textContent = isOpen ? '▼' : '▲';
    }

    function switchLang(lang) {
      renderQA(lang);
    }

    // 預設語言
    window.onload = () => renderQA('zh');
  </script>
</body>
</html>
