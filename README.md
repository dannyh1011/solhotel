<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>飯店QA</title>
  <style>
    html, body {
      margin: 0; padding: 0;
      background-color: #1a1616;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      display: flex; flex-direction: column; align-items: center;
      height: 100vh;
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
      transition: background-color 0.3s;
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
      max-height: 85vh;
      -webkit-overflow-scrolling: touch;
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
      user-select: none;
      transition: background-color 0.3s;
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
      color: #fff;
      background-color: #3a3a3a;
      border-radius: 8px;
      padding: 0 16px;
      line-height: 1.6;
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
      .question {
        font-size: 1.1rem;
        padding: 8px 12px;
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

  <div class="qa-container" id="qa"></div>

  <script>
    const qaData = {
      zh: [
        {
          q: "飯店周邊是否有夜市？",
          a: `▪ 每日：城隍廟夜市：<a href="https://www.google.com/maps?q=新竹市城隍廟夜市" target="_blank" style="color: #00bcd4;">點我查看地圖</a><br>
           ▪ 週二、週四：新竹後站夜市：<a href="https://www.google.com/maps?q=新竹後站夜市" target="_blank" style="color: #00bcd4;">點我查看地圖</a><br> 
          ▪ 週三、週五：樹林頭夜市：<a href="https://www.google.com/maps?q=樹林頭夜市" target="_blank" style="color: #00bcd4;">點我查看地圖</a>`

        },
        {
          q: "有哪些古蹟與觀光景點？",
          a: `
▪ 新竹州圖書館：<a href="https://maps.example.com/library" target="_blank">地圖</a><br>
▪ 東門迎曦門：<a href="https://maps.example.com/eastgate" target="_blank">地圖</a><br>
▪ 辛志平校長故居：<a href="https://maps.example.com/principalhouse" target="_blank">地圖</a><br>
▪ 新竹市影像博物館：<a href="https://maps.example.com/museum" target="_blank">地圖</a><br>
▪ 新竹市美術館：<a href="https://maps.example.com/artmuseum" target="_blank">地圖</a><br>
▪ 東門市場：<a href="https://maps.example.com/eastmarket" target="_blank">地圖</a><br>
▪ 新竹市政府：<a href="https://maps.example.com/cityhall" target="_blank">地圖</a><br>
▪ 新竹市消防博物館：<a href="https://maps.example.com/firemuseum" target="_blank">地圖</a><br>
▪ 新竹動物園：<a href="https://maps.example.com/zoo" target="_blank">地圖</a><br>
▪ 新竹公園：<a href="https://maps.example.com/park" target="_blank">地圖</a>`
        },
        {
          q: "有哪些宮廟？",
          a: `
▪ 東寧宮：<a href="https://maps.example.com/dongning" target="_blank">地圖</a><br>
▪ 新竹都城隍廟：<a href="https://maps.example.com/citygod" target="_blank">地圖</a><br>
▪ 新竹長和宮：<a href="https://maps.example.com/changhe" target="_blank">地圖</a><br>
▪ 關帝廟：<a href="https://maps.example.com/guandi" target="_blank">地圖</a>`
        },
        {
          q: "附近有哪裡可以購物？",
          a: `
▪ 巨城購物中心：<a href="https://maps.example.com/bigcity" target="_blank">地圖</a><br>
▪ 新竹大遠百：<a href="https://maps.example.com/farcity" target="_blank">地圖</a>`
        },
        {
          q: "Ubike在哪裡？",
          a: `
▪ 新竹市政府Ubike站：<a href="https://maps.example.com/ubike" target="_blank">地圖</a>`
        },
        {
          q: "早餐推薦？",
          a: `
▪ 古拉爵早餐：<a href="https://maps.example.com/breakfast1" target="_blank">地圖</a><br>
▪ 山東早點：<a href="https://maps.example.com/breakfast2" target="_blank">地圖</a><br>
▪ 星巴克-新竹州圖門市：<a href="https://maps.example.com/starbucks" target="_blank">地圖</a>`
        },
        {
          q: "咖啡和下午茶推薦？",
          a: `
▪ 星巴克-新竹州圖門市：<a href="https://maps.example.com/starbucks" target="_blank">地圖</a><br>
▪ 九幕咖啡：<a href="https://maps.example.com/coffee1" target="_blank">地圖</a><br>
▪ 饅饅好食：<a href="https://maps.example.com/coffee2" target="_blank">地圖</a><br>
▪ 一百種味道(三民店)：<a href="https://maps.example.com/coffee3" target="_blank">地圖</a><br>
▪ 夏.咖啡：<a href="https://maps.example.com/coffee4" target="_blank">地圖</a><br>
▪ Float Dept.微生咖啡：<a href="https://maps.example.com/coffee5" target="_blank">地圖</a>`
        },
        {
          q: "中式餐廳推薦？",
          a: `
▪ 菜園上海餐廳：<a href="https://maps.example.com/chinese1" target="_blank">地圖</a><br>
▪ 享鴨烤鴨：<a href="https://maps.example.com/chinese2" target="_blank">地圖</a><br>
▪ 西市汕頭館：<a href="https://maps.example.com/chinese3" target="_blank">地圖</a><br>
▪ 新橋弄堂：<a href="https://maps.example.com/chinese4" target="_blank">地圖</a>`
        },
        {
          q: "西式餐廳推薦？",
          a: `
▪ 冪2 La Miette Kitchen：<a href="https://maps.example.com/western1" target="_blank">地圖</a><br>
▪ TABLE JOE 喬桌子廚房：<a href="https://maps.example.com/western2" target="_blank">地圖</a><br>
▪ 史坦利美式牛排：<a href="https://maps.example.com/western3" target="_blank">地圖</a><br>
▪ 金色三麥 新竹巨城店PARK15：<a href="https://maps.example.com/western4" target="_blank">地圖</a>`
        },
        {
          q: "日式餐廳推薦？",
          a: `
▪ 柚子：<a href="https://maps.example.com/japanese1" target="_blank">地圖</a><br>
▪ 皿富器食 minfood：<a href="https://maps.example.com/japanese2" target="_blank">地圖</a><br>
▪ 橋燒肉府後店：<a href="https://maps.example.com/japanese3" target="_blank">地圖</a><br>
▪ 私嚐串燒：<a href="https://maps.example.com/japanese4" target="_blank">地圖</a><br>
▪ 大阪燒肉 燒魂Yakikon：<a href="https://maps.example.com/japanese5" target="_blank">地圖</a>`
        },
        {
          q: "素食餐廳推薦？",
          a: `
▪ 活原素Ｖ：<a href="https://maps.example.com/vegan1" target="_blank">地圖</a><br>
▪ 籽田野菜屋：<a href="https://maps.example.com/vegan2" target="_blank">地圖</a><br>
▪ 井家：<a href="https://maps.example.com/vegan3" target="_blank">地圖</a><br>
▪ 井町日式蔬食料理(大同店)：<a href="https://maps.example.com/vegan4" target="_blank">地圖</a><br>
▪ 八二親食-三民店：<a href="https://maps.example.com/vegan5" target="_blank">地圖</a>`
        },
        {
          q: "印度及異國料理推薦？",
          a: `
▪ 點22港式點心：<a href="https://maps.example.com/foreign1" target="_blank">地圖</a><br>
▪ 蘇丹土耳其廚房：<a href="https://maps.example.com/foreign2" target="_blank">地圖</a><br>
▪ 達達印度料理：<a href="https://maps.example.com/foreign3" target="_blank">地圖</a><br>
▪ MAS India Restaurant 媽媽印度料理：<a href="https://maps.example.com/foreign4" target="_blank">地圖</a>`
        },
        {
          q: "牛肉麵推薦？",
          a: `
▪ 段純貞牛肉麵：<a href="https://maps.example.com/beefnoodle1" target="_blank">地圖</a><br>
▪ 熊川牛肉麵：<a href="https://maps.example.com/beefnoodle2" target="_blank">地圖</a><br>
▪ 璽子牛肉麵（博愛店）：<a href="https://maps.example.com/beefnoodle3" target="_blank">地圖</a><br>
▪ 貳壹村精緻麵點：<a href="https://maps.example.com/beefnoodle4" target="_blank">地圖</a>`
        },
        {
          q: "推薦小吃？",
          a: `
▪ 喜劇收場(漢堡)：<a href="https://maps.example.com/snack1" target="_blank">地圖</a><br>
▪ 戲棚下Under Six Pound炸雞：<a href="https://maps.example.com/snack2" target="_blank">地圖</a><br>
▪ 覓雪Mixshare手作雪花冰：<a href="https://maps.example.com/snack3" target="_blank">地圖</a>`
        },
        {
          q: "伴手禮推薦？",
          a: `
▪ 福源花生醬：<a href="https://maps.example.com/gift1" target="_blank">地圖</a><br>
▪ 新復珍：<a href="https://maps.example.com/gift2" target="_blank">地圖</a><br>
▪ 淵明餅舖：<a href="https://maps.example.com/gift3" target="_blank">地圖</a><br>
▪ 進益貢丸：<a href="https://maps.example.com/gift4" target="_blank">地圖</a><br>
▪ 海瑞貢丸：<a href="https://maps.example.com/gift5" target="_blank">地圖</a>`
        }
      ],
      en: [
        {
          q: "What night markets are nearby?",
          a: `
▪ Shulintou Night Market: <a href="https://maps.example.com/shulintou" target="_blank">View Map</a><br>
▪ Back Station Night Market: <a href="https://maps.example.com/backstation" target="_blank">View Map</a>`
        },
        {
          q: "What historic sites and attractions are nearby?",
          a: `
▪ Hsinchu State Library: <a href="https://maps.example.com/library" target="_blank">Map</a><br>
▪ East Gate Yingxi Gate: <a href="https://maps.example.com/eastgate" target="_blank">Map</a><br>
▪ Principal Xin Zhiping's Former Residence: <a href="https://maps.example.com/principalhouse" target="_blank">Map</a><br>
▪ Hsinchu Image Museum: <a href="https://maps.example.com/museum" target="_blank">Map</a><br>
▪ Hsinchu Art Museum: <a href="https://maps.example.com/artmuseum" target="_blank">Map</a><br>
▪ East Gate Market: <a href="https://maps.example.com/eastmarket" target="_blank">Map</a><br>
▪ Hsinchu City Hall: <a href="https://maps.example.com/cityhall" target="_blank">Map</a><br>
▪ Hsinchu Fire Museum: <a href="https://maps.example.com/firemuseum" target="_blank">Map</a><br>
▪ Hsinchu Zoo: <a href="https://maps.example.com/zoo" target="_blank">Map</a><br>
▪ Hsinchu Park: <a href="https://maps.example.com/park" target="_blank">Map</a>`
        },
        {
          q: "What temples are nearby?",
          a: `
▪ Dongning Temple: <a href="https://maps.example.com/dongning" target="_blank">Map</a><br>
▪ Hsinchu City God Temple: <a href="https://maps.example.com/citygod" target="_blank">Map</a><br>
▪ Changhe Temple: <a href="https://maps.example.com/changhe" target="_blank">Map</a><br>
▪ Guandi Temple: <a href="https://maps.example.com/guandi" target="_blank">Map</a>`
        },
        {
          q: "Where can I shop nearby?",
          a: `
▪ Big City Shopping Center: <a href="https://maps.example.com/bigcity" target="_blank">Map</a><br>
▪ Far Eastern Department Store Hsinchu: <a href="https://maps.example.com/farcity" target="_blank">Map</a>`
        },
        {
          q: "Where is the Ubike station?",
          a: `
▪ Hsinchu City Hall Ubike Station: <a href="https://maps.example.com/ubike" target="_blank">Map</a>`
        },
        {
          q: "Where can I have breakfast?",
          a: `
▪ Garlic & Jazz Breakfast: <a href="https://maps.example.com/breakfast1" target="_blank">Map</a><br>
▪ Shandong Breakfast: <a href="https://maps.example.com/breakfast2" target="_blank">Map</a><br>
▪ Starbucks - Hsinchu State Library Store: <a href="https://maps.example.com/starbucks" target="_blank">Map</a>`
        },
        {
          q: "Coffee and afternoon tea recommendations?",
          a: `
▪ Starbucks - Hsinchu State Library Store: <a href="https://maps.example.com/starbucks" target="_blank">Map</a><br>
▪ Jiumu Coffee: <a href="https://maps.example.com/coffee1" target="_blank">Map</a><br>
▪ Manman Delicious: <a href="https://maps.example.com/coffee2" target="_blank">Map</a><br>
▪ Hundred Flavors (Sanmin Store): <a href="https://maps.example.com/coffee3" target="_blank">Map</a><br>
▪ Summer Coffee: <a href="https://maps.example.com/coffee4" target="_blank">Map</a><br>
▪ Float Dept. Micro Roastery: <a href="https://maps.example.com/coffee5" target="_blank">Map</a>`
        },
        {
          q: "Chinese restaurant recommendations?",
          a: `
▪ Vegetable Garden Shanghai Restaurant: <a href="https://maps.example.com/chinese1" target="_blank">Map</a><br>
▪ Enjoy Duck Roasted Duck: <a href="https://maps.example.com/chinese2" target="_blank">Map</a><br>
▪ Xishi Shantou Restaurant: <a href="https://maps.example.com/chinese3" target="_blank">Map</a><br>
▪ New Bridge Alley: <a href="https://maps.example.com/chinese4" target="_blank">Map</a>`
        },
        {
          q: "Western restaurant recommendations?",
          a: `
▪ La Miette Kitchen: <a href="https://maps.example.com/western1" target="_blank">Map</a><br>
▪ TABLE JOE Kitchen: <a href="https://maps.example.com/western2" target="_blank">Map</a><br>
▪ Stanley American Steakhouse: <a href="https://maps.example.com/western3" target="_blank">Map</a><br>
▪ Jinse Sanmai Park15, Hsinchu Big City: <a href="https://maps.example.com/western4" target="_blank">Map</a>`
        },
        {
          q: "Japanese restaurant recommendations?",
          a: `
▪ Yuzu: <a href="https://maps.example.com/japanese1" target="_blank">Map</a><br>
▪ Minfood: <a href="https://maps.example.com/japanese2" target="_blank">Map</a><br>
▪ Bridge Yakiniku Rear Store: <a href="https://maps.example.com/japanese3" target="_blank">Map</a><br>
▪ Private Taste Skewers: <a href="https://maps.example.com/japanese4" target="_blank">Map</a><br>
▪ Osaka Yakiniku Yakikon: <a href="https://maps.example.com/japanese5" target="_blank">Map</a>`
        },
        {
          q: "Vegetarian restaurant recommendations?",
          a: `
▪ Huoyuan Vegan V: <a href="https://maps.example.com/vegan1" target="_blank">Map</a><br>
▪ Zitian Vegetable House: <a href="https://maps.example.com/vegan2" target="_blank">Map</a><br>
▪ Jingjia: <a href="https://maps.example.com/vegan3" target="_blank">Map</a><br>
▪ Jingmachi Japanese Vegetarian (Datong Store): <a href="https://maps.example.com/vegan4" target="_blank">Map</a><br>
▪ 82 Qin Shi - Sanmin Store: <a href="https://maps.example.com/vegan5" target="_blank">Map</a>`
        },
        {
          q: "Indian and international cuisine recommendations?",
          a: `
▪ Dim 22 Hong Kong Dim Sum: <a href="https://maps.example.com/foreign1" target="_blank">Map</a><br>
▪ Sultan Turkish Kitchen: <a href="https://maps.example.com/foreign2" target="_blank">Map</a><br>
▪ Dada Indian Cuisine: <a href="https://maps.example.com/foreign3" target="_blank">Map</a><br>
▪ MAS India Restaurant: <a href="https://maps.example.com/foreign4" target="_blank">Map</a>`
        },
        {
          q: "Beef noodle recommendations?",
          a: `
▪ Duan Chun Zhen Beef Noodles: <a href="https://maps.example.com/beefnoodle1" target="_blank">Map</a><br>
▪ Xiongchuan Beef Noodles: <a href="https://maps.example.com/beefnoodle2" target="_blank">Map</a><br>
▪ Xi Zi Beef Noodles (Bo’ai Store): <a href="https://maps.example.com/beefnoodle3" target="_blank">Map</a><br>
▪ Er Yi Cun Exquisite Noodles: <a href="https://maps.example.com/beefnoodle4" target="_blank">Map</a>`
        },
        {
          q: "Snack recommendations?",
          a: `
▪ Comedy Ending (Burger): <a href="https://maps.example.com/snack1" target="_blank">Map</a><br>
▪ Under Six Pound Fried Chicken: <a href="https://maps.example.com/snack2" target="_blank">Map</a><br>
▪ Mixshare Handmade Shaved Ice: <a href="https://maps.example.com/snack3" target="_blank">Map</a>`
        },
        {
          q: "Souvenir recommendations?",
          a: `
▪ Fuyuan Peanut Butter: <a href="https://maps.example.com/gift1" target="_blank">Map</a><br>
▪ Xin Fuzhen: <a href="https://maps.example.com/gift2" target="_blank">Map</a><br>
▪ Yuanming Bakery: <a href="https://maps.example.com/gift3" target="_blank">Map</a><br>
▪ Jinyi Meatballs: <a href="https://maps.example.com/gift4" target="_blank">Map</a><br>
▪ Hairui Meatballs: <a href="https://maps.example.com/gift5" target="_blank">Map</a>`
        }
      ],
      ja: [
        {
          q: "夜市はどこですか？",
          a: `
▪ 樹林頭夜市：<a href="https://maps.example.com/shulintou" target="_blank">地図を見る</a><br>
▪ 後火車駅夜市：<a href="https://maps.example.com/backstation" target="_blank">地図を見る</a>`
        },
        {
          q: "歴史的建造物と観光スポットは？",
          a: `
▪ 新竹州図書館：<a href="https://maps.example.com/library" target="_blank">地図</a><br>
▪ 東門迎曦門：<a href="https://maps.example.com/eastgate" target="_blank">地図</a><br>
▪ 辛志平校長旧宅：<a href="https://maps.example.com/principalhouse" target="_blank">地図</a><br>
▪ 新竹市映像博物館：<a href="https://maps.example.com/museum" target="_blank">地図</a><br>
▪ 新竹市美術館：<a href="https://maps.example.com/artmuseum" target="_blank">地図</a><br>
▪ 東門市場：<a href="https://maps.example.com/eastmarket" target="_blank">地図</a><br>
▪ 新竹市政府：<a href="https://maps.example.com/cityhall" target="_blank">地図</a><br>
▪ 新竹市消防博物館：<a href="https://maps.example.com/firemuseum" target="_blank">地図</a><br>
▪ 新竹動物園：<a href="https://maps.example.com/zoo" target="_blank">地図</a><br>
▪ 新竹公園：<a href="https://maps.example.com/park" target="_blank">地図</a>`
        },
        {
          q: "近くの宮廟は？",
          a: `
▪ 東寧宮：<a href="https://maps.example.com/dongning" target="_blank">地図</a><br>
▪ 新竹都城隍廟：<a href="https://maps.example.com/citygod" target="_blank">地図</a><br>
▪ 新竹長和宮：<a href="https://maps.example.com/changhe" target="_blank">地図</a><br>
▪ 関帝廟：<a href="https://maps.example.com/guandi" target="_blank">地図</a>`
        },
        {
          q: "ショッピングはどこでできますか？",
          a: `
▪ 巨城ショッピングセンター：<a href="https://maps.example.com/bigcity" target="_blank">地図</a><br>
▪ 新竹大遠百：<a href="https://maps.example.com/farcity" target="_blank">地図</a>`
        },
        {
          q: "Ubikeの場所は？",
          a: `
▪ 新竹市政府Ubikeステーション：<a href="https://maps.example.com/ubike" target="_blank">地図</a>`
        },
        {
          q: "朝食のおすすめは？",
          a: `
▪ ガーリック＆ジャズ朝食：<a href="https://maps.example.com/breakfast1" target="_blank">地図</a><br>
▪ 山東の朝ごはん：<a href="https://maps.example.com/breakfast2" target="_blank">地図</a><br>
▪ スターバックス - 新竹州図書館店：<a href="https://maps.example.com/starbucks" target="_blank">地図</a>`
        },
        {
          q: "コーヒーとアフタヌーンティーのおすすめは？",
          a: `
▪ スターバックス - 新竹州図書館店：<a href="https://maps.example.com/starbucks" target="_blank">地図</a><br>
▪ 九幕コーヒー：<a href="https://maps.example.com/coffee1" target="_blank">地図</a><br>
▪ 饅饅好食：<a href="https://maps.example.com/coffee2" target="_blank">地図</a><br>
▪ 百の味（三民店）：<a href="https://maps.example.com/coffee3" target="_blank">地図</a><br>
▪ 夏コーヒー：<a href="https://maps.example.com/coffee4" target="_blank">地図</a><br>
▪ Float Dept.微生コーヒー：<a href="https://maps.example.com/coffee5" target="_blank">地図</a>`
        },
        {
          q: "中華料理店のおすすめは？",
          a: `
▪ 菜園上海料理店：<a href="https://maps.example.com/chinese1" target="_blank">地図</a><br>
▪ 享鴨ローストダック：<a href="https://maps.example.com/chinese2" target="_blank">地図</a><br>
▪ 西市汕頭館：<a href="https://maps.example.com/chinese3" target="_blank">地図</a><br>
▪ 新橋弄堂：<a href="https://maps.example.com/chinese4" target="_blank">地図</a>`
        },
        {
          q: "西洋料理店のおすすめは？",
          a: `
▪ 冪2 La Miette キッチン：<a href="https://maps.example.com/western1" target="_blank">地図</a><br>
▪ TABLE JOE キッチン：<a href="https://maps.example.com/western2" target="_blank">地図</a><br>
▪ スタンリーアメリカンステーキハウス：<a href="https://maps.example.com/western3" target="_blank">地図</a><br>
▪ 金色三麥 新竹巨城店 PARK15：<a href="https://maps.example.com/western4" target="_blank">地図</a>`
        },
        {
          q: "和食レストランのおすすめは？",
          a: `
▪ 柚子：<a href="https://maps.example.com/japanese1" target="_blank">地図</a><br>
▪ 皿富器食 minfood：<a href="https://maps.example.com/japanese2" target="_blank">地図</a><br>
▪ 橋焼肉府後店：<a href="https://maps.example.com/japanese3" target="_blank">地図</a><br>
▪ 私嚐串焼：<a href="https://maps.example.com/japanese4" target="_blank">地図</a><br>
▪ 大阪焼肉 燒魂Yakikon：<a href="https://maps.example.com/japanese5" target="_blank">地図</a>`
        },
        {
          q: "ベジタリアンレストランのおすすめは？",
          a: `
▪ 活原素Ｖ：<a href="https://maps.example.com/vegan1" target="_blank">地図</a><br>
▪ 籽田野菜屋：<a href="https://maps.example.com/vegan2" target="_blank">地図</a><br>
▪ 井家：<a href="https://maps.example.com/vegan3" target="_blank">地図</a><br>
▪ 井町日式蔬食料理（大同店）：<a href="https://maps.example.com/vegan4" target="_blank">地図</a><br>
▪ 八二親食-三民店：<a href="https://maps.example.com/vegan5" target="_blank">地図</a>`
        },
        {
          q: "インド料理・エスニック料理のおすすめは？",
          a: `
▪ 点22香港点心：<a href="https://maps.example.com/foreign1" target="_blank">地図</a><br>
▪ スルタン・トルコ料理店：<a href="https://maps.example.com/foreign2" target="_blank">地図</a><br>
▪ ダダ・インド料理：<a href="https://maps.example.com/foreign3" target="_blank">地図</a><br>
▪ MASインドレストラン：<a href="https://maps.example.com/foreign4" target="_blank">地図</a>`
        },
        {
          q: "牛肉麺のおすすめは？",
          a: `
▪ 段純貞牛肉麺：<a href="https://maps.example.com/beefnoodle1" target="_blank">地図</a><br>
▪ 熊川牛肉麺：<a href="https://maps.example.com/beefnoodle2" target="_blank">地図</a><br>
▪ 璽子牛肉麺（博愛店）：<a href="https://maps.example.com/beefnoodle3" target="_blank">地図</a><br>
▪ 貳壹村精緻麺点：<a href="https://maps.example.com/beefnoodle4" target="_blank">地図</a>`
        },
        {
          q: "おすすめの軽食は？",
          a: `
▪ 喜劇終了（バーガー）：<a href="https://maps.example.com/snack1" target="_blank">地図</a><br>
▪ 劇場下アンダーシックスパウンド唐揚げ：<a href="https://maps.example.com/snack2" target="_blank">地図</a><br>
▪ ミックスシェア手作りかき氷：<a href="https://maps.example.com/snack3" target="_blank">地図</a>`
        },
        {
          q: "お土産のおすすめは？",
          a: `
▪ 福源ピーナッツバター：<a href="https://maps.example.com/gift1" target="_blank">地図</a><br>
▪ 新復珍：<a href="https://maps.example.com/gift2" target="_blank">地図</a><br>
▪ 淵明餅舗：<a href="https://maps.example.com/gift3" target="_blank">地図</a><br>
▪ 進益貢丸：<a href="https://maps.example.com/gift4" target="_blank">地図</a><br>
▪ 海瑞貢丸：<a href="https://maps.example.com/gift5" target="_blank">地図</a>`
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
        question.innerHTML = `・${item.q} <span class="arrow">${index === 0 ? '▲' : '▼'}</span>`;
        question.onclick = () => toggleAnswer(index);

        const answer = document.createElement('div');
        answer.className = 'answer';
        answer.innerHTML = item.a;

        if(index === 0) answer.classList.add('open');

        qaItem.appendChild(question);
        qaItem.appendChild(answer);
        container.appendChild(qaItem);
      });
    }

    function toggleAnswer(index) {
      const answers = document.querySelectorAll('.answer');
      const arrows = document.querySelectorAll('.arrow');

      answers.forEach((answer, i) => {
        const isCurrent = i === index;
        if(isCurrent) {
          if(answer.classList.contains('open')) {
            answer.classList.remove('open');
            arrows[i].textContent = '▼';
          } else {
            answer.classList.add('open');
            arrows[i].textContent = '▲';
          }
        } else {
          answer.classList.remove('open');
          arrows[i].textContent = '▼';
        }
      });
    }

    function switchLang(lang) {
      renderQA(lang);
    }

    // 預設載入中文
    renderQA('zh');
  </script>
</body>
</html>
</body>
</html>
