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
      width: 100%;
      max-width: 800px; /* 電腦最大寬度 */
      margin: 0 20px;   /* 左右留空，手機桌面都適用 */
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
          q: " 📢 飯店公告訊息 ",
          a: `日前無公告訊息。</a>`
        },
         {
          q: "🅿️停車資訊🚗",
          a: `
▪🅿️1 館內停車場停: 位於地下一樓（限高2.2米），停放後請搭乘電梯至一樓櫃檯登記入住。<br><br>
▪若館內停車場停滿，您另可停放至距離飯店步行5分鐘的二個公有停車場，並請於退房時間11：00前於櫃檯索取停車時數抵用後再行取車。
<a href="https://drive.google.com/file/d/1hSUqt1-tvvqJNq6W8Hk1pWYlmPOG_dCY/view" target="_blank">➡️停車場地圖⬅️</a><br><br>
▪🅿️2 東大陸橋下停車場-中央站：半露天・平面停車場</a><br>
▪🅿️3 府後停車場： 地下室・室內停車場</a><br><br>

⭐ 新春及週末尖峰時段，停車需求量大，如遇等待車位狀況，造成您的不便，敬請見諒。<br>
⭐ 團體及特殊優惠專案，"不提供" 停車時數抵用。<br>
⭐ 車位僅供館內住宿客人停放，非住客停放須收取$500元停車費用。<br>
⭐ 本館停車場無附設充電設施。</a>`
        },

      
        {
          q: "🚶飯店周邊古蹟景點",
          a: `
▪ 新竹州圖書館：<a href="https://www.google.com/maps?q=新竹州圖書館" target="_blank">地圖</a><br>
▪ 東門迎曦門：<a href="https://www.google.com/maps?q=東門迎曦門" target="_blank">地圖</a><br>
▪ 辛志平校長故居：<a href="https://www.google.com/maps?q=辛志平校長故居" target="_blank">地圖</a><br>
▪ 新竹市影像博物館：<a href="https://www.google.com/maps?q=新竹市影像博物館" target="_blank">地圖</a><br>
▪ 新竹市美術館：<a href="https://www.google.com/maps?q=新竹市美術館" target="_blank">地圖</a><br>
▪ 東門市場：<a href="https://www.google.com/maps?q=東門市場" target="_blank">地圖</a><br>
▪ 新竹市政府：<a href="https://www.google.com/maps?q=新竹市政府" target="_blank">地圖</a><br>
▪ 新竹市消防博物館：<a href="https://www.google.com/maps?q=新竹市消防博物館" target="_blank">地圖</a><br>
▪ 國立新竹生活美學館（原新竹公會堂）：<a href="https://www.google.com/maps?q=國立新竹生活美學館（原新竹公會堂）" target="_blank">地圖</a><br>
▪ 新竹動物園：<a href="https://www.google.com/maps?q=新竹動物園" target="_blank">地圖</a><br>
▪ 新竹公園：<a href="https://www.google.com/maps?q=新竹公園" target="_blank">地圖</a>`
        },
        {
          q: "飯店鄰近夜市",
          a: `▪ 🚶每日：城隍廟夜市：<a href="https://www.google.com/maps?q=新竹市城隍廟夜市" target="_blank">地圖</a><br>
           ▪ 🚶週二、週五：新竹後站夜市：<a href="https://www.google.com/maps?q=新竹後站夜市" target="_blank">地圖</a><br>
         ▪ 🚕週六、週日 11:00~19:00：新竹假日花市：<a href="https://www.google.com/maps?q=新竹假日花市" target="_blank">地圖</a>`
        },
         {
          q: "🚕新竹觀光景點",
          a: `
▪ 🚶新竹都城隍廟：<a href="https://www.google.com/maps?q=新竹都城隍廟" target="_blank">地圖</a><br>
▪ 🚶新竹公園：<a href="https://www.google.com/maps?q=新竹公園 都會公園" target="_blank">地圖</a><br>
▪ 🚶新竹市立動物園：<a href="https://www.google.com/maps?q=新竹市立動物園" target="_blank">地圖</a><br>
▪ 🚶新竹市玻璃工藝博物館：<a href="https://www.google.com/maps?q=新竹市玻璃工藝博物館" target="_blank">地圖</a><br>
▪ 將軍村：<a href="https://www.google.com/maps?q=將軍村" target="_blank">地圖</a><br>
▪ 市定古蹟-新竹水道取水口展示館(周一及周五戲水池清潔消毒不開放)：<a href="https://www.google.com/maps?q=市定古蹟-新竹水道取水口展示館(周一及周五戲水池清潔消毒不開放)" target="_blank">地圖</a><br>
▪ 青草湖：<a href="https://www.google.com/maps?q=青草湖" target="_blank">地圖</a><br>
▪ 青青草原：<a href="https://www.google.com/maps?q=青青草原 香山" target="_blank">地圖</a><br>
▪ 新竹(南寮漁港)17公里海岸風景區：<a href="https://www.google.com/maps?q=新竹17公里海岸風景區" target="_blank">地圖</a><br>
▪ 南寮魚鱗天梯：<a href="https://www.google.com/maps?q=南寮魚鱗天梯" target="_blank">地圖</a><br>
▪ 香山濕地賞蟹步道：<a href="https://www.google.com/maps?q=香山濕地賞蟹步道" target="_blank">地圖</a><br>
▪ 香山車站：<a href="https://www.google.com/maps?q=香山車站" target="_blank">地圖</a><br>
▪ 風情海岸：<a href="https://www.google.com/maps?q=風情海岸" target="_blank">地圖</a>`
        },
        {
          q: "飯店周邊宮廟景點",
          a: `
▪ 🚶東寧宮：<a href="https://www.google.com/maps?q=東寧宮" target="_blank">地圖</a><br>
▪ 🚶新竹都城隍廟：<a href="https://www.google.com/maps?q=新竹都城隍廟" target="_blank">地圖</a><br>
▪ 新竹竹蓮寺：<a href="https://www.google.com/maps?q=新竹竹蓮寺" target="_blank">地圖</a><br>
▪ 新竹長和宮：<a href="https://www.google.com/maps?q=新竹長和宮" target="_blank">地圖</a><br>
▪ 新竹天公壇：<a href="https://www.google.com/maps?q=新竹天公壇" target="_blank">地圖</a><br>
▪ 關帝廟：<a href="https://www.google.com/maps?q=新竹關帝廟 南門街" target="_blank">地圖</a>`
        },
        {
          q: "鄰近購物百貨",
          a: `
▪ 🚶巨城購物中心：<a href="https://www.google.com/maps?q=巨城購物中心" target="_blank">地圖</a><br>
▪ 🚕大魯閣湳雅廣場：<a href="https://www.google.com/maps?q=大魯閣湳雅廣場" target="_blank">地圖</a><br>
▪ 新竹大遠百：<a href="https://www.google.com/maps?q=新竹大遠百" target="_blank">地圖</a>`
        },
        {
          q: "鄰近YouBike單車借用站🚴",
          a: `
⚠️YouBike使用說明：<a href="https://www.youbike.com.tw/region/main/" target="_blank"> YouBike官網</a><br>
▪ 🚶新竹市政府YouBike站 <a href="https://www.google.com/maps?q=YouBike 新竹市政府" target="_blank">地圖</a>`
        },
         {
          q: "台灣鐵路・高速鐵路・機場捷運<br>・桃園機場・松山機場✈️　",
          a: `
▪ 🚶台灣鐵路：<a href="https://www.railway.gov.tw/tra-tip-web/tip?lang=ZH_TW" target="_blank"> 台鐵官網</a><br>
▪ 台灣高鐵：<a href="https://www.thsrc.com.tw/" target="_blank"> 高鐵官網</a><br>
▪ 桃園捷運/機場捷運：<a href="https://www.tymetro.com.tw/tymetro-new/tw/index.php" target="_blank"> 機捷官網</a><br>
▪ 桃園國際機場：<a href="https://www.taoyuan-airport.com/" target="_blank"> 桃機官網</a><br>
▪ 台北松山機場：<a href="https://www.tsa.gov.tw/" target="_blank">松山機場</a>`
        },

 {
          q: "迎曦飯店 → 桃園國際機場✈️ 交通方式?　",
          a: `
▪ 台灣高鐵：<br>新竹高鐵站 → 桃園高鐵站 → 機場捷運 → 桃園機場。<br>⏱ 約 80–90 分鐘 💰約NT$300-$500<br><br>
▪ 🚶客運：<br>搭乘 日豪客運 1250 機場巴士，「新竹轉運站」直達桃園國際機場。<br>⏱ 約 90–100 分鐘 💰約NT$200。<br><br>
➡️日豪客運：<br><a href="https://www.taiwanbus.tw/eBUSPage/Query/QueryResult.aspx?rno=12500&rn=1755744773691&lan=C" target="_blank"> 公路客運即時動態資訊網</a><br>
➡️新竹轉運站：<a href="https://www.google.com/maps?q=新竹轉運站" target="_blank">地圖</a><br><br>
▪ 計程車：<br>從飯店直達桃園國際機場。<br>⏱ 約 50–60 分鐘 💰約NT$1430 ~ NT$1600`
        },
        
         {
          q: "南寮漁港・清華大學・交通大學🚌交通方式?",
          a: `
▪ 南寮漁港-新竹客運0150_藍15區公車：<a href="http://www.hcbus.com.tw/big5/information-2.asp?select=7&button=%E9%80%81%E5%87%BA" target="_blank"> 新竹客運官網</a><br>
▪ 清華大學雙校區-科技之星83路公車：<a href="https://www.yosemite-bus.com.tw/no81_bus.asp#no83" target="_blank"> 科技之星官網</a><br>
▪ 交通大學雙校區、清華大學光復校區-新竹客運0020_2路公車：<a href="http://www.hcbus.com.tw/big5/information-2.asp?select=2&button=%E9%80%81%E5%87%BA" target="_blank"> 新竹客運官網</a>`
        },
        {
          q: "🚶鄰近早餐店",
          a: `
▪ 義式屋古拉爵：<a href="https://www.google.com/maps?q=義式屋古拉爵 新竹迎曦店" target="_blank">地圖</a><br>
▪ 山東早點-眷村龎：<a href="https://www.google.com/maps?q=眷村龎"target="_blank">地圖</a><br>
▪ 薯霸早餐：<a href="https://www.google.com/maps?q=薯霸早餐"target="_blank">地圖</a><br>
▪ 星巴克-新竹州圖門市：<a href="https://www.google.com/maps?q=星巴克-新竹州圖門市" target="_blank">地圖</a>`
        },
        {
          q: "咖啡☕和下午茶",
          a: `
▪ 🚶星巴克-新竹州圖門市：<a href="https://www.google.com/maps?q=星巴克-新竹州圖門市" target="_blank">地圖</a><br>
▪ 🚶THE FOX COFFEE CLUB：<a href="https://www.google.com/maps?q=THE FOX COFFEE CLUB" target="_blank">地圖</a><br>
▪ 🚶九幕咖啡：<a href="https://www.google.com/maps?q=九幕咖啡" target="_blank">地圖</a><br>
▪ 🚶MANO MANO | 新州屋門市：<a href="https://www.google.com/maps?q=MANO MANO | 新州屋門市" target="_blank">地圖</a><br>
▪ 種甜：<a href="https://www.google.com/maps?q=種甜" target="_blank">地圖</a><br>
▪ Hidden off：<a href="https://www.google.com/maps?q=Hidden off" target="_blank">地圖</a><br>
▪ 一想一響咖啡：<a href="https://www.google.com/maps?q=一想一響咖啡" target="_blank">地圖</a><br>
▪ 李克承博士故居 a-moom：<a href="https://www.google.com/maps?q=李克承博士故居 a-moom(新竹市)" target="_blank">地圖</a><br>
▪ 春室 SPRING POOL GLASS STUDIO + The POOL：<a href="https://www.google.com/maps?q=春室 SPRING POOL GLASS STUDIO + The POOL" target="_blank">地圖</a><br>
▪ Louisa Coffee 路易莎咖啡 (新竹公園門市)：<a href="https://www.google.com/maps?q=Louisa Coffee 路易莎咖啡  新竹東區公園路" target="_blank">地圖</a><br>
▪ 墨咖啡 INK COFFEE：<a href="https://www.google.com/maps?q=墨咖啡 INK COFFEE" target="_blank">地圖</a><br>
▪ 🚶饅饅好食：<a href="https://www.google.com/maps?q=饅饅好食" target="_blank">地圖</a><br>
▪ 一百種味道 (三民店)：<a href="https://www.google.com/maps?q=一百種味道(三民店)" target="_blank">地圖</a><br>
▪ 🚶夏.咖啡：<a href="https://www.google.com/maps?q=夏.咖啡 仁愛街" target="_blank">地圖</a><br>
▪ 🚶Float Dept.微生咖啡：<a href="https://www.google.com/maps?q=Float Dept.微生咖啡" target="_blank">地圖</a>`
        },
{
          q: "台式餐廳🏅",
          a: `
▪ 蔡記燒酒雞：<a href="https://www.google.com/maps?q=蔡記燒酒雞" target="_blank">地圖</a><br>
▪ 🚶東門米粉攤（新竹東門市場店）・🏅2025必比登：<a href="https://www.google.com/maps?q=東門米粉攤（新竹東門市場店" target="_blank">地圖</a><br>
▪ 🚶原味鴨肉麵・🏅2025必比登：<a href="https://www.google.com/maps?q=原味鴨肉麵 勝利路" target="_blank">地圖</a><br>
▪ 石坊小井：<a href="https://www.google.com/maps?q=石坊小井" target="_blank">地圖</a><br>
▪ 🚶一二三台灣料理：<a href="https://www.google.com/maps?q=一二三台灣料理" target="_blank">地圖</a><br>
▪ 新馬辣經典麻辣鍋-新竹巨城店：<a href="https://www.google.com/maps?q=新馬辣經典麻辣鍋-新竹巨城店" target="_blank">地圖</a><br>
▪ 🚕禾日香古早味魯肉飯・🏅2025必比登：<a href="https://www.google.com/maps?q=禾日香古早味魯肉飯" target="_blank">地圖</a><br>
▪ 🚕貓的堅持（新竹店）創意輕藥膳養生料理・🏅2025必比登：<a href="https://www.google.com/maps?q=貓的堅持（新竹店）創意輕藥膳養生料理" target="_blank">地圖</a><br>
▪ 🚕漢王薑母鴨 新竹林森路：<a href="https://www.google.com/maps?q=漢王薑母鴨 新竹林森路" target="_blank">地圖</a><br>
▪ 🚕鼎泰豐 新竹店：<a href="https://www.google.com/maps?q=鼎泰豐 新竹店" target="_blank">地圖</a><br>
▪ 🚕竹東邱記排骨酥麵-新竹店：<a href="https://www.google.com/maps?q=竹東邱記排骨酥麵-新竹店" target="_blank">地圖</a><br>
▪ 🚶中大水餃鍋貼館：<a href="https://www.google.com/maps?q=中大水餃鍋貼館" target="_blank">地圖</a><br>
▪ 🚶龍昌小館：<a href="https://www.google.com/maps?q=龍昌小館" target="_blank">地圖</a>`
        },
        
        {
          q: "🚶中式餐廳🏅",
          a: `
▪ 菜園上海餐廳・🏅2025必比登：<a href="https://www.google.com/maps?q=菜園上海餐廳" target="_blank">地圖</a><br>
▪ 享鴨烤鴨：<a href="https://www.google.com/maps?q=享鴨 烤鴨與中華料理 新竹北大店" target="_blank">地圖</a><br>
▪ 西市汕頭館：<a href="https://www.google.com/maps?q=西市汕頭館 北大店" target="_blank">地圖</a><br>
▪ 🚕海底撈火鍋・新竹：<a href="https://www.google.com/maps?q=海底撈火鍋 新竹" target="_blank">地圖</a><br>
▪ 新陶芳・客家菜：<a href="https://www.google.com/maps?q=新陶芳 東大路" target="_blank">地圖</a><br>

▪ 🚕弄味小廚・客家菜・🏅2025必比登：<a href="https://www.google.com/maps?q=弄味小廚 客家菜系" target="_blank">地圖</a><br>
▪ 新橋弄堂：<a href="https://www.google.com/maps?q=新橋弄堂" target="_blank">地圖</a>`
        },
        {
          q: "🚶西式🥩、義大利餐廳",
          a: `
▪ 冪2 La Miette Kitchen：<a href="https://www.google.com/maps?q=冪2 La Miette Kitchen" target="_blank">地圖</a><br>
▪ Friendy Pizzeria：<a href="https://www.google.com/maps?q=Friendy Pizzeria" target="_blank">地圖</a><br>
▪ 🚕SPASSO披薩：<a href="https://www.google.com/maps?q=SPASSO" target="_blank">地圖</a><br>
▪ 🚕Go eat Tapas Dining BAR 西班牙餐酒館：<a href="https://www.google.com/maps?q=Go eat Tapas Dining BAR 西班牙餐酒館" target="_blank">地圖</a><br>
▪ TABLE JOE 喬桌子廚房：<a href="https://www.google.com/maps?q=TABLE JOE 喬桌子廚房" target="_blank">地圖</a><br>
▪ 史坦利美式牛排🥩：<a href="https://www.google.com/maps?q=史坦利美式牛排 巨城" target="_blank">地圖</a><br>
▪ EISEN BISTRO 艾昇小館：<a href="https://www.google.com/maps?q=EISEN BISTRO 艾昇小館" target="_blank">地圖</a><br>
▪ 金色三麥 新竹巨城店PARK15：<a href="https://www.google.com/maps?q=金色三麥 新竹巨城店PARK15" target="_blank">地圖</a>`
        },
        {
          q: "🚶日式餐廳",
          a: `
▪ 柚子：<a href="https://www.google.com/maps?q=柚子 文化街" target="_blank">地圖</a><br>
▪ 皿富器食 minfood：<a href="https://www.google.com/maps?q=皿富器食 minfood" target="_blank">地圖</a><br>
▪ 京町家日式串燒🍢居酒屋：<a href="https://www.google.com/maps?q=京町家日式串燒居酒屋"_blank">地圖</a><br>
▪ 横浜家系ラーメン拉麵家：<a href="https://www.google.com/maps?q=横浜家系ラーメン拉麵家"_blank">地圖</a><br>
▪ ラーメン 鷄白湯：<a href="https://www.google.com/maps?q=ラーメン 鷄白湯"_blank">地圖</a><br>
▪ 隱川居酒屋_いざかや：<a href="https://www.google.com/maps?q=隱川居酒屋_いざかや" target="_blank">地圖</a><br>
▪ 和食川上日本料理🍣：<a href="https://www.google.com/maps?q=和食川上日本料理"_blank">地圖</a><br>
▪ 麺宮浦島 ：<a href="https://www.google.com/maps?q=麺宮浦島"_blank">地圖</a><br>
▪ 福氣廚房🍣-新竹世界店：<a href="https://www.google.com/maps?q=福氣廚房-新竹世界店"_blank">地圖</a><br>
▪ 🚕Musha Musha 熟成咖哩：<a href="https://www.google.com/maps?q=Musha Musha 熟成咖哩 武昌" target="_blank">地圖</a><br>
▪ 🚕新竹燒肉 (モルディブ馬爾地夫)本店🍖：<a href="https://www.google.com/maps?q=新竹燒肉 モルディブ馬爾地夫本店" target="_blank">地圖</a><br>
▪ 新橋燒肉屋🍖：<a href="https://www.google.com/maps?q=新橋燒肉屋 府後店" target="_blank">地圖</a><br>
▪ 私嚐串燒🍢：<a href="https://www.google.com/maps?q=私嚐串燒 中正店"_blank">地圖</a><br>
▪ 大阪燒肉 燒魂Yakikon🍖：<a href="https://www.google.com/maps?q=大阪燒肉 燒魂Yakikon 新竹市東區" target="_blank">地圖</a>`
        },
        {
          q: "🚶素食🥗餐廳",
          a: `
▪ 果庭蔬食廚房：<a href="https://www.google.com/maps?q=果庭蔬食廚房" target="_blank">地圖</a><br>
▪ 森活原素 V-Element 蔬食餐廳：<a href="https://www.google.com/maps?q=森活原素 V-Element 蔬食餐廳" target="_blank">地圖</a><br>
▪ 籽田野菜屋：<a href="https://www.google.com/maps?q=籽田野菜屋" target="_blank">地圖</a><br>
▪ 井家：<a href="https://www.google.com/maps?q=井家" target="_blank">地圖</a><br>
▪ 井町日式蔬食料理(大同店)：<a href="https://www.google.com/maps?q=井町日式蔬食料理 大同店" target="_blank">地圖</a><br>
▪ 八二親食-三民店：<a href="https://www.google.com/maps?q=八二親食-三民店" target="_blank">地圖</a>`
        },
        {
          q: "印度料理與國際美食",
          a: `
▪ 🚶132官舍餐酒館Bistro：<a href="https://www.google.com/maps?q=132官舍/新竹州警務部部長官舍(餐酒館Bistro)" target="_blank">地圖</a><br>
▪ 蔣好的味道 (台越小吃)：<a href="https://www.google.com/maps?q=蔣好的味道 台越特色小館" target="_blank">地圖</a><br>
▪ 艷麗Pondok Sunny(星馬料理)：<a href="https://www.google.com/maps?q=艷麗Pondok Sunny" target="_blank">地圖</a><br>
▪ 🚶青丹扎西(西藏料理)東門市場店：<a href="https://www.google.com/maps?q=青丹扎西 東門市場店" target="_blank">地圖</a><br>
▪ El Mundo墨多：<a href="https://www.google.com/maps?q=El Mundo墨多" target="_blank">地圖</a><br>
▪ 蘇丹土耳其廚房：<a href="https://www.google.com/maps?q=蘇丹土耳其廚房" target="_blank">地圖</a><br>
▪ 🚶東京純豆腐新竹SOGO店(韓式)：<a href="https://www.google.com/maps?q=東京純豆腐Tokyo Sundubu 新竹SOGO店" target="_blank">地圖</a><br>
▪ 🚶姜滿堂존맛탱 新竹巨城店：<a href="https://www.google.com/maps?q=姜滿堂존맛탱 新竹巨城店" target="_blank">地圖</a><br>
▪ 達達印度料理：<a href="https://www.google.com/maps?q=達達印度料理(新竹店)(原 印度小鎮)Burans Indian Kitchen in Hsinchu (Indian Town)" target="_blank">地圖</a><br>
▪ 🚶美陽光印度餐廳：<a href="https://www.google.com/maps?q=美陽光印度餐廳Sunshine Indian Restaurant Hsinchu" target="_blank">地圖</a><br>
▪ 淇里思印度餐廳 新竹店：<a href="https://www.google.com/maps?q=淇里思 新竹店" target="_blank">Map</a><br>
▪ MAS India Restaurant 媽媽印度料理：<a href="https://www.google.com/maps?q=MAS India Restaurant 媽媽印度料理" target="_blank">地圖</a>`
        },
        {
          q: "牛肉麵🐂🍜🏅",
          a: `
▪ 段純貞牛肉麵：<a href="https://www.google.com/maps?q=段純貞牛肉麵新竹市北區武陵路" target="_blank">地圖</a><br>
▪ 🚶九添福牛肉麵館新竹城隍店・🏅2025必比登：<a href="https://www.google.com/maps?q=九添福牛肉麵館新竹城隍店" target="_blank">地圖</a><br>
▪ 🚶熊川牛肉麵：<a href="https://www.google.com/maps?q=熊川牛肉麵" target="_blank">地圖</a><br>
▪ 璽子牛肉麵（博愛店）：<a href="https://www.google.com/maps?q=璽子牛肉麵（博愛店)" target="_blank">地圖</a><br>
▪ 貳壹村精緻麵點：<a href="https://www.google.com/maps?q=貳壹村精緻麵點" target="_blank">地圖</a>`
        },
        {
          q: "🚶小吃資訊",
          a: `
▪ 🚶喜劇收場(漢堡)：<a href="https://www.google.com/maps?q=喜劇收場(漢堡)" target="_blank">地圖</a><br>
▪ 🚶戲棚下Under Six Pound炸雞：<a href="https://www.google.com/maps?q=戲棚下Under Six Pound炸雞" target="_blank">地圖</a><br>
▪ 🚶覓雪Mixshare手作雪花冰：<a href="https://www.google.com/maps?q=覓雪Mixshare手作雪花冰" target="_blank">地圖</a><br>
▪ 白色麥芽餅茯苓糕（米滋食舖）：<a href="https://www.google.com/maps?q=白色麥芽餅茯苓糕（米滋食舖）" target="_blank">地圖</a><br>
▪ 🚶好豆味冰沙豆花：<a href="https://www.google.com/maps?q=好豆味冰沙豆花 勝利路" target="_blank">地圖</a><br>
▪ 🚕河堤上的貓 (手搖飲)：<a href="https://www.google.com/maps?q=河堤上的貓" target="_blank">地圖</a><br>
▪ 山田麻糬製造所：<a href="https://www.google.com/maps?q=山田麻糬製造所" target="_blank">地圖</a><br>
▪ 原夜市鴨肉麵：<a href="https://www.google.com/maps?q=原夜市鴨肉麵 中央路" target="_blank">地圖</a><br>
▪ 薪石窯柴燒窯烤麵包：<a href="https://www.google.com/maps?q=薪石窯柴燒窯烤麵包" target="_blank">地圖</a><br>
▪ 廟口鴨香飯：<a href="https://www.google.com/maps?q=廟口鴨香飯 中山路" target="_blank">地圖</a>`
        },
        {
          q: "伴手禮🎁",
          a: `
▪ 🚶福源花生醬：<a href="https://www.google.com/maps?q=福源花生醬 新竹市東區東大路一段" target="_blank">地圖</a><br>
▪ 🚶新復珍商行(竹塹餅・米粉)：<a href="https://www.google.com/maps?q=新復珍商行" target="_blank">地圖</a><br>
▪ 🚶淵明餅舖(水蒸蛋糕)：<a href="https://www.google.com/maps?q=淵明餅舖" target="_blank">地圖</a><br>
▪ 德龍水潤餅：<a href="https://www.google.com/maps?q=德龍水潤餅" target="_blank">地圖</a><br>
▪ 進益貢丸：<a href="https://www.google.com/maps?q=進益貢丸新竹市北區北門街"_blank">地圖</a><br>
▪ 海瑞貢丸：<a href="https://www.google.com/maps?q=海瑞貢丸新竹西門總店"_blank">地圖</a>`
        }
      ],
      en: [
         {
          q: " 📢 Hotel Announcements ",
          a: `No announcements at the moment.</a>`
        },
       
        {
          q: "🚶Historical sites and attractions near the hotel",
          a: `
▪ Hsinchu State Library: <a href="https://www.google.com/maps?q=新竹州圖書館" target="_blank">Map</a><br>
▪ East Gate Yingxi Gate: <a href="https://www.google.com/maps?q=東門迎曦門" target="_blank">Map</a><br>
▪ Principal Xin Zhiping's Former Residence: <a href="https://www.google.com/maps?q=辛志平校長故居"  target="_blank">Map</a><br>
▪ Hsinchu Image Museum: <a href="https://www.google.com/maps?q=新竹市影像博物館" target="_blank">Map</a><br>
▪ Hsinchu Art Museum: <a href="https://www.google.com/maps?q=新竹市美術館" target="_blank">Map</a><br>
▪ East Gate Market: <a href="https://www.google.com/maps?q=東門市場" target="_blank">Map</a><br>
▪ Hsinchu City Hall: <a href="https://www.google.com/maps?q=新竹市政府" target="_blank">Map</a><br>
▪ Hsinchu Fire Museum: <a href="https://www.google.com/maps?q=新竹市消防博物館" target="_blank">Map</a><br>
▪ National Hsinchu Living Arts Center (Former Hsinchu Public Hall)：<a href="https://www.google.com/maps?q=國立新竹生活美學館（原新竹公會堂）" target="_blank">Map</a><br>
▪ Hsinchu Zoo: <a href="https://www.google.com/maps?q=新竹動物園" target="_blank">Map</a><br>
▪ Hsinchu Park: <a href="https://www.google.com/maps?q=新竹公園" target="_blank">Map</a>`
        },
         {
          q: "Nearby Night Markets",
          a:  `▪ 🚶Daily – Chenghuang Temple Night Market – <a href="https://www.google.com/maps?q=新竹市城隍廟夜市" target="_blank">Map</a><br><br>
           ▪ 🚶Tuesday and Friday – Hsinchu Back Station Night Market: <a href="https://www.google.com/maps?q=新竹後站夜市"  target="_blank">Map</a><br><br>
            ▪ 🚕Saturday and Sunday 11:00~19:00：Holiday Flower Market：<a href="https://www.google.com/maps?q=新竹假日花市" target="_blank">Map</a>`
        },
         {
          q: "Tourist Attractions in Hsinchu",
          a: `
▪ 🚶Hsinchu Chenghuang Temple：<a href="https://www.google.com/maps?q=新竹都城隍廟" target="_blank">Map</a><br>
▪ 🚶Hsinchu Park：<a href="https://www.google.com/maps?q=新竹公園 都會公園" target="_blank">Map</a><br>
▪ 🚶Hsinchu City Zoo：<a href="https://www.google.com/maps?q=新竹市立動物園" target="_blank">Map</a><br>
▪ 🚶Hsinchu Glass Museum：<a href="https://www.google.com/maps?q=新竹市玻璃工藝博物館" target="_blank">Map</a><br>
▪ General’s Village：<a href="https://www.google.com/maps?q=將軍村" target="_blank">Map</a><br>
▪ Hsinchu Waterway Intake Exhibition Hall (Splash pools closed for cleaning and disinfection on Mondays and Fridays)：<a href="https://www.google.com/maps?q=市定古蹟-新竹水道取水口展示館(周一及周五戲水池清潔消毒不開放)" target="_blank">Map</a><br>
▪ Qingcao Lake (Green Grass Lake)：<a href="https://www.google.com/maps?q=青草湖" target="_blank">Map</a><br>
▪ Qingqing Grassland：<a href="https://www.google.com/maps?q=青青草原 香山" target="_blank">Map</a><br>
▪ Hsinchu (Nanliao Fishing Harbor) 17 km Coastal Scenic Area：<a href="https://www.google.com/maps?q=新竹17公里海岸風景區" target="_blank">Map</a><br>
▪ Xiangshan Wetland Crab Viewing Trail：<a href="https://www.google.com/maps?q=香山濕地賞蟹步道" target="_blank">Map</a><br>
▪ Fengqing Coast：<a href="https://www.google.com/maps?q=風情海岸" target="_blank">Map</a><br>
⭐ Hsinchu City Travel Info：<a href="https://eng.taiwan.net.tw/m1.aspx?sno=0002109" target="_blank">Tourism Administration</a>`
        },
        {
          q: "Temple attractions near the hotel",
          a: `
▪ 🚶Dongning Temple: <a href="https://www.google.com/maps?q=東寧宮" target="_blank">Map</a><br>
▪ 🚶Hsinchu City God Temple: <a href="https://www.google.com/maps?q=新竹都城隍廟" target="_blank">Map</a><br>
▪ Hsinchu Zhulin Temple：<a href="https://www.google.com/maps?q=新竹竹蓮寺" target="_blank">Map</a><br>
▪ Changhe Temple: <a href="https://www.google.com/maps?q=新竹長和宮" target="_blank">Map</a><br>
▪ Hsinchu Tiangong Temple ：<a href="https://www.google.com/maps?q=新竹天公壇" target="_blank">Map</a><br>
▪ Guandi Temple: <a href="https://www.google.com/maps?q=新竹關帝廟 南門街" target="_blank">Map</a>`
        },
        {
          q: "Nearby shopping malls",
          a: `
▪ 🚶Big City Shopping Center: <a href="https://www.google.com/maps?q=巨城購物中心" target="_blank">Map</a><br>
▪ 🚕Taroko Nanya Plaza：<a href="https://www.google.com/maps?q=大魯閣湳雅廣場" target="_blank">Map</a><br>
▪ Far Eastern Department Store Hsinchu: <a href="https://www.google.com/maps?q=新竹大遠百" target="_blank">Map</a>`
        },
        {
          q: "Nearby YouBike rental station🚴",
          a: `
         ⚠️Before signing up, please prepare the following. <a href="https://en.youbike.com.tw/region/main/register/" target="_blank"> YouBike official website</a><br><br>
▪ 🚶Hsinchu City Hall Ubike Station: <a href="https://www.google.com/maps?q=YouBike 新竹市政府" target="_blank">Map</a>`
        },
         {
          q: "Taiwan Railways Administration (TRA)🚆<br>・Airport MRT🚆<br>・High Speed Rail(HSR)🚄<br>・Taoyuan International Airport(TPE)✈️<br>・Taipei Songshan Airport(TSA)✈️",
          a: `
▪ Taiwan Railways Administration (TRA) ：<a href="https://tip.railway.gov.tw/tra-tip-web/tip?lang=EN_US" target="_blank"> official website</a><br>
▪ Taiwan High Speed Rail(HSR)：<a href="https://en.thsrc.com.tw/"_blank"> official website</a><br>
▪ Taoyuan Metro・Airport MRT：<a href="https://www.tymetro.com.tw/tymetro-new/en/index.php" target="_blank"> official website</a><br>
▪ Taoyuan International Airport(TPE)：<a href="https://www.taoyuan-airport.com/?lang=en" target="_blank"> official website</a><br>
▪ Taipei Songshan Airport(TSA)：<a href="https://www.tsa.gov.tw/?id=ef81d612-6ca0-4e0f-9459-30bfb8c9523f&culture=2" target="_blank">official website</a>`
        },

        {
          q: "SOL Hotel → Taoyuan International Airport✈️?　",
          a: `
▪ Taiwan High Speed Rail(HSR)：<br>Hsinchu HSR → Taoyuan HSR → Airport MRT → Airport <br>⏱ About 80–90 min 💰About NT$300–500<br><br>
▪ Taxi：<br>SOL Hotel → Taoyuan International Airport <br>⏱ About 50–60 min 💰About NT$1430 ~ NT$1600`
        },
        
        {
          q: "🚶Nearby breakfast shops",
          a: `
▪ Garlic & Jazz Breakfast: <a href="https://www.google.com/maps?q=義式屋古拉爵 新竹迎曦店" target="_blank">Map</a><br>
▪ Shandong Breakfast - Xiao Long Bao (steamed soup dumplings), Taiwanese egg crepes: <a href="https://www.google.com/maps?q=眷村龎" target="_blank">Map</a><br>
▪ Shuba Breakfast：<a href="https://www.google.com/maps?q=薯霸早餐"target="_blank">Map</a><br>
▪ Starbucks - Hsinchu State Library Store:<a href="https://www.google.com/maps?q=星巴克-新竹州圖門市" target="_blank">Map</a>`
        },
        {
          q: "Coffee☕ and afternoon tea",
          a: `
▪ 🚶Starbucks - Hsinchu State Library Store: <a href="https://www.google.com/maps?q=星巴克-新竹州圖門市" target="_blank">Map</a><br>
▪ 🚶THE FOX COFFEE CLUB：<a href="https://www.google.com/maps?q=THE FOX COFFEE CLUB" target="_blank">Map</a><br>
▪ 🚶Jiumu Coffee: <a href="https://www.google.com/maps?q=九幕咖啡" target="_blank">Map</a><br>
▪ 🚶MANO MANO：<a href="https://www.google.com/maps?q=MANO MANO | 新州屋門市" target="_blank">Map</a><br>
▪ 🚶Seed Sweet Coffee(No Fixed Holidays)：<a href="https://www.google.com/maps?q=種甜" target="_blank">Map</a><br>
▪ Hidden off：<a href="https://www.google.com/maps?q=Hidden off" target="_blank">Map</a><br>
▪ ReEcho Coffee：<a href="https://www.google.com/maps?q=一想一響咖啡" target="_blank">Map</a><br>
▪ Former Residence of Dr. Lee Ko-Cheng (A-Moom)：<a href="https://www.google.com/maps?q=李克承博士故居 a-moom(新竹市)" target="_blank">Map</a><br>
▪ Spring Room SPRING POOL GLASS STUDIO + The POOL：<a href="https://www.google.com/maps?q=春室 SPRING POOL GLASS STUDIO + The POOL" target="_blank">Map</a><br>
▪ Louisa Coffee (Hsinchu Park Branch)：<a href="https://www.google.com/maps?q=Louisa Coffee 路易莎咖啡  新竹東區公園路" target="_blank">Map</a><br>
▪ Ink Coffee：<a href="https://www.google.com/maps?q=墨咖啡 INK COFFEE" target="_blank">Map</a><br>
▪ 🚶Manman Delicious: <a href="https://www.google.com/maps?q=饅饅好食" target="_blank">Map</a><br>
▪ 🚶Hundred Flavors (Sanmin Store): <a href="https://www.google.com/maps?q=一百種味道(三民店)" target="_blank">Map</a><br>
▪ 🚶Summer Coffee: <a href="https://www.google.com/maps?q=夏.咖啡 仁愛街" target="_blank">Map</a><br>
▪ 🚶Float Dept. Micro Roastery: <a href="https://www.google.com/maps?q=Float Dept.微生咖啡" target="_blank">Map</a>`
        },
{
          q: "Taiwanese Restaurants🏅",
          a: `
▪ Tsai Ji Sesame Oil Chicken：<a href="https://www.google.com/maps?q=蔡記燒酒雞" target="_blank">Map</a><br>
▪ 🚶Dongmen Rice Noodle Stall・🏅2025 Michelin Bib Gourmand：<a href="https://www.google.com/maps?q=東門米粉攤（新竹東門市場店）" target="_blank">Map</a><br>
▪ 🚶Original Flavor Duck Noodles・🏅2025必比登：<a href="https://www.google.com/maps?q=原味鴨肉麵 勝利路" target="_blank">Map</a><br>
▪ Shifang Xiaojing：<a href="https://www.google.com/maps?q=石坊小井" target="_blank">Map</a><br>
▪ 🚶123 Taiwanese Cuisine：<a href="https://www.google.com/maps?q=一二三台灣料理" target="_blank">Map</a><br>
▪ Xin Mala Classic Hot Pot(Spicy Sichuan Hot Pot)：<a href="https://www.google.com/maps?q=新馬辣經典麻辣鍋-新竹巨城店" target="_blank">Map</a><br>
▪ 🚕Herixiang Traditional Braised Pork Rice・🏅2025 Michelin Bib Gourmand：<a href="https://www.google.com/maps?q=禾日香古早味魯肉飯" target="_blank">Map</a><br>
▪ 🚕Cat’s Persistence (Hsinchu Branch) ・ Creative Light Herbal Health Cuisine・🏅2025 Michelin Bib Gourmand：<a href="https://www.google.com/maps?q=貓的堅持（新竹店）創意輕藥膳養生料理" target="_blank">地圖</a><br>
▪ 🚕Han Wang Ginger Duck：<a href="https://www.google.com/maps?q=漢王薑母鴨 新竹林森路" target="_blank">Map</a><br>
▪ 🚕Din Tai Fung(Soup Dumplings)：<a href="https://www.google.com/maps?q=鼎泰豐 新竹店" target="_blank">Map</a><br>
▪ 🚶Zhongda Dumpling & Potstickers Restaurant：<a href="https://www.google.com/maps?q=中大水餃鍋貼館" target="_blank">Map</a><br>
▪ 🚶Long Chang Bistro：<a href="https://www.google.com/maps?q=龍昌小館" target="_blank">Map</a>`
        },
        
        {
          q: "🚶Chinese restaurants🏅",
          a: `
▪ Vegetable Garden Shanghai Restaurant・🏅2025 Michelin Bib Gourmand: <a href="https://www.google.com/maps?q=菜園上海餐廳" target="_blank">Map</a><br>
▪ Enjoy Duck Roasted Duck: <a href="https://www.google.com/maps?q=享鴨 烤鴨與中華料理 新竹北大店" target="_blank">Map</a><br>
▪ Xishi Shantou Restaurant: <a href="https://www.google.com/maps?q=西市汕頭館 北大店" target="_blank">Map</a><br>
▪ Xin Taofang ・ Hakka Cuisine：<a href="https://www.google.com/maps?q=新陶芳 東大路" target="_blank">Map</a><br>
▪ 🚕 Haidilao Hot Pot：<a href="https://www.google.com/maps?q=海底撈火鍋 新竹" target="_blank">Map</a><br>
▪ 🚕 Nongwei Bistro・Hakka Cuisine・🏅2025 Michelin Bib Gourmand<a href="https://www.google.com/maps?q=弄味小廚 客家菜系" target="_blank">Map</a><br>
▪ New Bridge Alley: <a href="https://www.google.com/maps?q=新橋弄堂"target="_blank">Map</a>`
        },
        {
          q: "🚶🥩Western restaurants",
          a: `
▪ La Miette Kitchen: <a href="https://www.google.com/maps?q=冪2 La Miette Kitchen" target="_blank">Map</a><br>
▪ Friendy Pizzeria：<a href="https://www.google.com/maps?q=Friendy Pizzeria" target="_blank">Map</a><br>
▪ 🚕SPASSO Pizza：<a href="https://www.google.com/maps?q=SPASSO" target="_blank">Map</a><br>
▪ 🚕Go eat Tapas Dining BAR – Spanish Restaurant & Bar：<a href="https://www.google.com/maps?q=Go eat Tapas Dining BAR 西班牙餐酒館" target="_blank">Map</a><br>
▪ TABLE JOE Kitchen: <a href="https://www.google.com/maps?q=TABLE JOE 喬桌子廚房" target="_blank">Map</a><br>
▪ Stanley American Steakhouse🥩:<a href="https://www.google.com/maps?q=史坦利美式牛排 巨城" target="_blank">Map</a><br>
▪ EISEN BISTRO：<a href="https://www.google.com/maps?q=EISEN BISTRO 艾昇小館" target="_blank">Map</a><br>
▪ Jinse Sanmai Park15, Hsinchu Big City: <a href="https://www.google.com/maps?q=金色三麥 新竹巨城店PARK15" target="_blank">Map</a>`
        },
        {
          q: "🚶Japanese restaurants",
          a: `
▪ Yuzu: <a href="https://www.google.com/maps?q=柚子 文化街" target="_blank">Map</a><br>
▪ Minfood:<a href="https://www.google.com/maps?q=皿富器食 minfood" target="_blank">Map</a><br>
▪ Kyoto Machiya Japanese Skewers🍢 Izakaya：<a href="https://www.google.com/maps?q=京町家日式串燒居酒屋"_blank">Map</a><br>
▪ Yokohama Iekei Ramen House：<a href="https://www.google.com/maps?q=横浜家系ラーメン拉麵家"_blank">Map</a><br>
▪ Ramen Chicken Paitan：<a href="https://www.google.com/maps?q=ラーメン 鷄白湯"_blank">Map</a><br>
▪ Musha Musha Curry：<a href="https://www.google.com/maps?q=Musha Musha 熟成咖哩 武昌" target="_blank">Map</a><br>
▪ Inkawa Izakaya：<a href="https://www.google.com/maps?q=隱川居酒屋_いざかや" target="_blank">Map</a><br>
▪ Fortune Kitchen🍣：<a href="https://www.google.com/maps?q=福氣廚房-新竹世界店"_blank">Map</a><br>
▪ Kawakami Japanese Cuisine🍣：<a href="https://www.google.com/maps?q=和食川上日本料理"_blank">Map</a><br>
▪ Menmiya Urashima：<a href="https://www.google.com/maps?q=麺宮浦島"_blank">Map</a><br>
▪ 🚕Hsinchu Yakiniku – Maldives🍖：<a href="https://www.google.com/maps?q=新竹燒肉 モルディブ馬爾地夫本店" target="_blank">Map</a><br>
▪ Shinbashi Yakiniku🍖: <a href="https://www.google.com/maps?q=新橋燒肉屋 府後店" target="_blank">Map</a><br>
▪ Private Taste Skewers🍢: <a href="https://www.google.com/maps?q=私嚐串燒 中正店" target="_blank">Map</a><br>
▪ Osaka Yakiniku Yakikon🍖: <a href="https://www.google.com/maps?q=大阪燒肉 燒魂Yakikon 新竹市東區" target="_blank">Map</a>`
        },
        {
          q: "🚶Vegetarian🥗 restaurants",
          a: `
▪ Guoting Vegetarian Kitchen：<a href="https://www.google.com/maps?q=果庭蔬食廚房" target="_blank">Map</a><br>
▪ V-Element Vegetarian Kitchen：<a href="https://www.google.com/maps?q=森活原素 V-Element 蔬食餐廳" target="_blank">Map</a><br>
▪ Zitian Vegetable House: <a href="https://www.google.com/maps?q=籽田野菜屋" target="_blank">Map</a><br>
▪ Jingjia:：<a href="https://www.google.com/maps?q=井町日式蔬食料理 大同店" target="_blank">Map</a><br>
▪ Jingmachi Japanese Vegetarian: <a href="https://www.google.com/maps?q=井家" target="_blank">Map</a><br>
▪ 82 Qin Shi: <a href="https://www.google.com/maps?q=八二親食-三民店" target="_blank">Map</a>`
        },
        {
          q: "Indian & International Cuisine",
          a: `
▪ 🚶132 Officer’s Residence Bistro：<a href="https://www.google.com/maps?q=132官舍/新竹州警務部部長官舍(餐酒館Bistro)" target="_blank">Map</a><br>
▪ Jiang’s Good Taste (Taiwanese & Vietnamese Eats)：<a href="https://www.google.com/maps?q=蔣好的味道 台越特色小館" target="_blank">Map</a><br>
▪ Yanli Pondok Sunny-Singaporean and Malaysian Cuisine：<a href="https://www.google.com/maps?q=艷麗Pondok Sunny" target="_blank">Map</a><br>
▪ 🚶Qingdan Zhaxi (Tibetan Cuisine)：<a href="https://www.google.com/maps?q=青丹扎西 東門市場店" target="_blank">Map</a><br>
▪ El Mundo Mexican Cuisine：<a href="https://www.google.com/maps?q=El Mundo墨多" target="_blank">Map</a><br>
▪ Sultan Turkish Kitchen: <a href="https://www.google.com/maps?q=蘇丹土耳其廚房" target="_blank">Map</a><br>
▪ 🚶Tokyo Sundubu Hsinchu SOGO Branch (Korean Cuisine)：<a href="https://www.google.com/maps?q=東京純豆腐Tokyo Sundubu 新竹SOGO店" target="_blank">Map</a><br>
▪ 🚶Jiang Man Tang Jonmattaeng (Korean Cuisine)：<a href="https://www.google.com/maps?q=姜滿堂존맛탱 新竹巨城店" target="_blank">Map</a><br>
▪ Dada Indian Cuisine: <a href="https://www.google.com/maps?q=達達印度料理(新竹店)(原 印度小鎮)Burans Indian Kitchen in Hsinchu (Indian Town)" target="_blank">Map</a><br>
▪ 🚶Sunshine Indian Restaurant：<a href="https://www.google.com/maps?q=美陽光印度餐廳Sunshine Indian Restaurant Hsinchu" target="_blank">Map</a><br>
▪ CHILLIESINE Indian Restaurantt：<a href="https://www.google.com/maps?q=淇里思 新竹店" target="_blank">Map</a><br>
▪ MAS India Restaurant:<a href="https://www.google.com/maps?q=MAS India Restaurant 媽媽印度料理" target="_blank">Map</a>`
        },
        {
          q: "Beef noodle🐂🍜🏅",
          a: `
▪ Duan Chun Zhen Beef Noodles: <a href="https://www.google.com/maps?q=段純貞牛肉麵新竹市北區武陵路" target="_blank">Map</a><br>
▪ 🚶Jiutianfu Beef Noodle Restaurant・🏅2025 Michelin Bib Gourmand：<a href="https://www.google.com/maps?q=九添福牛肉麵館新竹城隍店" target="_blank">Map</a><br>
▪ 🚶Xiongchuan Beef Noodles: <a href="https://www.google.com/maps?q=熊川牛肉麵" target="_blank">Map</a><br>
▪ Xi Zi Beef Noodles: <a href="https://www.google.com/maps?q=璽子牛肉麵（博愛店)" target="_blank">Map</a><br>
▪ Er Yi Cun Exquisite Noodles: <a href="https://www.google.com/maps?q=貳壹村精緻麵點" target="_blank">Map</a>`
        },
        {
          q: "Snack Information",
          a: `
▪ 🚶Comedy Ending (Burger): <a href="https://www.google.com/maps?q=喜劇收場(漢堡)" target="_blank">Map</a><br>
▪ 🚶Under Six Pound Fried Chicken : <a href="https://www.google.com/maps?q=戲棚下Under Six Pound炸雞" target="_blank">Map</a><br>
▪ 🚶Mixshare Handmade Shaved Ice : <a href="https://www.google.com/maps?q=覓雪Mixshare手作雪花冰" target="_blank">Map</a><br>
▪ White Malt Cake & Poria Cake：<a href="https://www.google.com/maps?q=白色麥芽餅茯苓糕（米滋食舖）" target="_blank">Map</a><br>
▪ 🚶Shaved Ice Tofu Pudding：<a href="https://www.google.com/maps?q=好豆味冰沙豆花 勝利路" target="_blank">Map</a><br>
▪ Yamada Mochi Factory：<a href="https://www.google.com/maps?q=山田麻糬製造所" target="_blank">Map</a><br>
▪ Duck Noodles：<a href="https://www.google.com/maps?q=原夜市鴨肉麵 中央路" target="_blank">Map</a><br>
▪ Duck Rice：<a href="https://www.google.com/maps?q=廟口鴨香飯 中山路" target="_blank">Map</a>`
        },
        {
          q: "Hsinchu Souvenirs🎁",
          a: `
▪ 🚶Fuyuan Peanut Butter: <a href="https://www.google.com/maps?q=福源花生醬 新竹市東區東大路一段" target="_blank">Map</a><br>
▪ 🚶Xin Fuzhen - Zhujian Cake・Rice Noodles: <a href="https://www.google.com/maps?q=新復珍商行" target="_blank">Map</a><br>
▪ 🚶Yuanming Bakery-Steamed Sponge Cake: <a href="https://www.google.com/maps?q=淵明餅舖" target="_blank">Map</a><br>
▪ Jinyi Meatballs: <a href="https://www.google.com/maps?q=進益貢丸新竹市北區北門街"_blank">Map</a><br>
▪ Hairui Meatballs: <a href="https://www.google.com/maps?q=海瑞貢丸新竹西門總店" target="_blank">Map</a>`
        }
      ],
      ja: [
        {
          q: " 📢 ホテルからのお知らせ ",                                                                           
          a: `現在お知らせはありません。</a>`
        },
        
        {
          q: "🚶ホテル周辺の史跡・観光スポット",
          a: `
▪ 新竹州図書館：<a href="https://www.google.com/maps?q=新竹州圖書館" target="_blank">地図</a><br>
▪ 東門迎曦門：<a href="https://www.google.com/maps?q=東門迎曦門" target="_blank">地図</a><br>
▪ 辛志平校長旧宅：<a href="https://www.google.com/maps?q=辛志平校長故居"  target="_blank">地図</a><br>
▪ 新竹市映像博物館：<a href="https://www.google.com/maps?q=新竹市影像博物館" target="_blank">地図</a><br>
▪ 新竹市美術館：<a href="https://www.google.com/maps?q=新竹市美術館" target="_blank">地図</a><br>
▪ 東門市場：<a href="https://www.google.com/maps?q=東門市場" target="_blank">地図</a><br>
▪ 新竹市政府：<a href="https://www.google.com/maps?q=新竹市政府" target="_blank">地図</a><br>
▪ 新竹市消防博物館：<a href="https://www.google.com/maps?q=新竹市消防博物館" target="_blank">地図</a><br>
▪ 国立新竹生活美学館（旧新竹公会堂）：<a href="https://www.google.com/maps?q=國立新竹生活美學館（原新竹公會堂）" target="_blank">地図</a><br>
▪ 新竹動物園：<a href="https://www.google.com/maps?q=新竹動物園" target="_blank">地図</a><br>
▪ 新竹公園：<a href="https://www.google.com/maps?q=新竹公園"_blank">地図</a>`
        },
        {
          q: "ホテル近くの夜市（よいち）",
          a: `▪🚶 毎日・城隍廟夜市（チョンホアンミャオ夜市）– <a href="https://www.google.com/maps?q=新竹市城隍廟夜市"  target="_blank">地図</a><br>
          ▪ 🚶火曜日・金曜日：新竹後駅夜市 – <a href="https://www.google.com/maps?q=新竹後站夜市"  target="_blank">地図</a><br>
          ▪ 🚕土曜日・日曜日 11:00~19:00：ホリデー花市場：<a href="https://www.google.com/maps?q=新竹假日花市" target="_blank">地図</a>`

        },
         {
          q: "新竹の観光スポット",
          a: `
▪ 🚶新竹都城隍廟：<a href="https://www.google.com/maps?q=新竹都城隍廟" target="_blank">地図</a><br>
▪ 🚶新竹公園：<a href="https://www.google.com/maps?q=新竹公園 都會公園" target="_blank">地図</a><br>
▪ 🚶新竹市立動物園：<a href="https://www.google.com/maps?q=新竹市立動物園" target="_blank">地図</a><br>
▪ 🚶新竹市ガラス工芸博物館：<a href="https://www.google.com/maps?q=新竹市玻璃工藝博物館" target="_blank">地図</a><br>
▪ 将軍村：<a href="https://www.google.com/maps?q=將軍村" target="_blank">地図</a><br>
▪ 新竹水道取水口展示館（月曜と金曜は水遊びプールの清掃消毒のため閉館）：<a href="https://www.google.com/maps?q=市定古蹟-新竹水道取水口展示館(周一及周五戲水池清潔消毒不開放)" target="_blank">地図</a><br>
▪ 青草湖：<a href="https://www.google.com/maps?q=青草湖" target="_blank">地図</a><br>
▪ 青青草原：<a href="https://www.google.com/maps?q=青青草原 香山" target="_blank">地図</a><br>
▪ 新竹（南寮漁港）17キロの海岸風景区：<a href="https://www.google.com/maps?q=新竹17公里海岸風景區" target="_blank">地図</a><br>
▪ 香山湿地のカニ観察歩道：<a href="https://www.google.com/maps?q=香山濕地賞蟹步道" target="_blank">地図</a><br>
▪ 風情海岸：<a href="https://www.google.com/maps?q=風情海岸" target="_blank">地図</a><br>
⭐ 新竹市旅行情報：<a href="https://jp.taiwan.net.tw/m1.aspx?sno=0003109" target="_blank">交通部観光署</a>`
        },
        {
          q: "ホテル周辺の寺院・神社スポット",
          a: `
▪ 🚶東寧宮：<a href="https://www.google.com/maps?q=東寧宮" target="_blank">地図</a><br>
▪ 🚶新竹都城隍廟：<a href="https://www.google.com/maps?q=新竹都城隍廟" target="_blank">地図</a><br>
▪ 新竹竹蓮寺：<a href="https://www.google.com/maps?q=新竹竹蓮寺" target="_blank">地図</a><br>
▪ 新竹長和宮：<a href="https://www.google.com/maps?q=新竹長和宮" target="_blank">地図</a><br>
▪ 新竹天公壇：<a href="https://www.google.com/maps?q=新竹天公壇" target="_blank">地図</a><br>
▪ 関帝廟：<a href="https://www.google.com/maps?q=新竹關帝廟 南門街" target="_blank">地図</a>`
        },
        {
          q: "近隣のショッピングモール",
          a: `
▪ 🚶巨城ショッピングセンター：<a href="https://maps.example.com/bigcity" target="_blank">地図</a><br>
▪ 🚕タロコ南雅プラザ：<a href="https://www.google.com/maps?q=大魯閣湳雅廣場" target="_blank">地図</a><br>
▪ 新竹大遠百：<a href="https://www.google.com/maps?q=新竹大遠百" target="_blank">地図</a>`
        },
        {
          q: "近くYouBikeレンタルステーション🚴",
          a: `
          ⚠️ご登録の前に、以下のものをご準備ください。<a href="https://en.youbike.com.tw/region/main/register/" target="_blank"> YouBike公式ウェブサイト-英語のみ</a><br><br>
▪ 🚶新竹市政府Ubikeステーション：<a href="https://www.google.com/maps?q=YouBike 新竹市政府" target="_blank">地図</a>`
        },
         {
          q: "台湾鉄路株式会社(TRA)🚆<br>・台湾高速鉄道(HSR)🚄<br>・桃園空港MRT🚆<br>・桃園國際機場(TPE)✈️<br>・台北松山機場(TSA)✈️",
          a: `
▪ 🚶台湾鉄路株式会社(TRA) ：<a href="https://tip.railway.gov.tw/tra-tip-web/tip?lang=JA_JP" target="_blank"> 公式ウェブサイト</a><br>
▪ 台湾高速鉄道(HSR)：<a href="https://jp.thsrc.com.tw/ArticleContent/07a7dfcc-1910-485f-a296-699ff11efb46"_blank"> 公式ウェブサイト</a><br>
▪ 桃園MRT・桃園空港MRT：<a href="https://www.tymetro.com.tw/tymetro-new/jp/index.php" target="_blank"> 公式ウェブサイト</a><br>
▪ 桃園國際機場(TPE)：<a href="https://www.taoyuan-airport.com/?lang=jp" target="_blank"> 公式ウェブサイト</a><br>
▪ 台北松山機場(TSA)：<a href="https://www.tsa.gov.tw/?culture=3"_blank">公式ウェブサイト</a>`
        },

        {
          q: "SOLホテル → 桃園国際空港✈️?　",
          a: `
▪ 台湾高速鉄道(HSR)：<br>新竹高鉄駅 → 桃園高鉄駅 → 空港MRT → 桃園空港 <br>⏱ 約80～90分 💰約NT$300-$500<br><br>
▪ タクシー：<br>ホテル → 桃園国際空港 <br>⏱ 約50～60分 💰約NT$1430 ~ NT$1600`
        },
  {
          q: "SOLホテル → 台北松山空港✈️?　",
          a: `
▪ 台湾高速鉄道(HSR)+MRT：<br>新竹高鉄駅 → 台北駅 → MRT板南線（青）→ 忠孝復興駅 → MRT文湖線（茶）に乗換 → 松山空港<br>⏱ 約90～100分 💰約NT$300-$500<br><br>
▪ 台湾鉄路会社(TRA)+MRT：<br>新竹駅（台鉄）→ 台北駅 → MRT板南線（青）→ 忠孝復興駅 → MRT文湖線（茶）に乗換 → 松山空港<br>⏱ 約120分～140分 💰約NT$200-$300<br><br>
▪ タクシー：<br>ホテル → 松山空港 <br>⏱ 約90分 💰約NT$2420 ~ NT$2800` 
        },        
        {
          q: "🚶近隣の朝食店",
          a: `
▪ ガーリック＆ジャズ朝食：<a href="https://www.google.com/maps?q=義式屋古拉爵 新竹迎曦店" target="_blank">地図</a><br>
▪ 山東の朝食・眷村龎 - 小籠包（ショウロンポー）、台湾式卵クレープ（ダンビン）：<a href="https://www.google.com/maps?q=眷村龎" target="_blank">地図</a><br>
▪ 薯霸ブレックファースト：<a href="https://www.google.com/maps?q=薯霸早餐"target="_blank">地図</a><br>
▪ スターバックス - 新竹州図書館店：<a href="https://www.google.com/maps?q=星巴克-新竹州圖門市" target="_blank">地図</a>`
        },
        {
          q: "コーヒー☕とアフタヌーンティー",
          a: `
▪ 🚶スターバックス -(Starbucks 新竹州図書館店)：<a href="https://www.google.com/maps?q=新竹州圖書館" target="_blank">地図</a><br>
▪ 🚶THE FOX COFFEE CLUB：<a href="https://www.google.com/maps?q=THE FOX COFFEE CLUB" target="_blank">地図</a><br>
▪ 🚶九幕コーヒー：<a href="https://www.google.com/maps?q=九幕咖啡" target="_blank">地図</a><br>
▪ 🚶MANO MANO：<a href="https://www.google.com/maps?q=MANO MANO | 新州屋門市" target="_blank">地図</a><br>
▪ 種甜 (不定休)：<a href="https://www.google.com/maps?q=種甜" target="_blank">地図</a><br>
▪ Hidden off：<a href="https://www.google.com/maps?q=Hidden off" target="_blank">Map</a><br>
▪ リ・エコー・コーヒー：<a href="https://www.google.com/maps?q=一想一響咖啡" target="_blank">地図</a><br>
▪ 李克承博士旧宅（エームーム・A-Moom)：<a href="https://www.google.com/maps?q=李克承博士故居 a-moom(新竹市)" target="_blank">地図</a><br>
▪ 春室 SPRING POOL GLASS STUDIO + The POOL：<a href="https://www.google.com/maps?q=春室 SPRING POOL GLASS STUDIO + The POOL" target="_blank">地図</a><br>
▪ ルイーザコーヒー（Louisa Coffee 新竹公園店）：<a href="https://www.google.com/maps?q=Louisa Coffee 路易莎咖啡  新竹東區公園路" target="_blank">地図</a><br>
▪ 墨咖啡 INK COFFEE：<a href="https://www.google.com/maps?q=墨咖啡 INK COFFEE" target="_blank">地図</a><br>
▪ 🚶饅饅好食：<a href="https://www.google.com/maps?q=饅饅好食" target="_blank">地図</a><br>
▪ 百の味（三民店）：<a href="https://www.google.com/maps?q=一百種味道(三民店)" target="_blank">地図</a><br>
▪ 🚶夏コーヒー：<a href="https://www.google.com/maps?q=夏.咖啡 仁愛街" target="_blank">地図</a><br>
▪ 🚶Float Dept.微生コーヒー：<a href="https://www.google.com/maps?q=Float Dept.微生咖啡" target="_blank">地図</a>`
        },
        {
          q: "台湾料理🥟🏅",
          a: `
▪ 蔡記 ヌーベル紹興酒鶏：<a href="https://www.google.com/maps?q=蔡記燒酒雞" target="_blank">地図</a><br>
▪ 🚶東門（トンメン）米粉屋・🏅2025 ミシュラン ビブグルマン：<a href="https://www.google.com/maps?q=東門米粉攤（新竹東門市場店）" target="_blank">地図</a><br>
▪ 🚶オリジナル味の鴨肉麺・🏅2025必比登：<a href="https://www.google.com/maps?q=原味鴨肉麵 勝利路" target="_blank">Map</a><br>
▪ 石坊小井：<a href="https://www.google.com/maps?q=石坊小井" target="_blank">地図</a><br>
▪ 🚶一二三台湾料理：<a href="https://www.google.com/maps?q=一二三台灣料理" target="_blank">地図</a><br>
▪ 新馬辣クラシック火鍋(マーラー火鍋)：<a href="https://www.google.com/maps?q=新馬辣經典麻辣鍋-新竹巨城店" target="_blank">地図</a><br>
▪ 🚕禾日香（ヘリシャン）ルーローハン・🏅2025 ミシュラン ビブグルマン：<a href="https://www.google.com/maps?q=禾日香古早味魯肉飯" target="_blank">地図</a><br>
▪ 🚕猫のこだわり（新竹店）・ 創意軽薬膳健康料理・🏅2025 ミシュラン ビブグルマン：<a href="https://www.google.com/maps?q=貓的堅持（新竹店）創意輕藥膳養生料理" target="_blank">地図</a><br>
▪ 🚕漢王ジンジャーダック：<a href="https://www.google.com/maps?q=漢王薑母鴨 新竹林森路" target="_blank">地図</a><br>
▪ 🚶中大（チュンダ）水餃子・鍋貼館：<a href="https://www.google.com/maps?q=中大水餃鍋貼館" target="_blank">地図</a><br><br>
▪ 🚕鼎泰豊・ディンタイフォン・台湾薄皮小籠包🥟（ショウロンポウ）：<a href="https://www.google.com/maps?q=鼎泰豐 新竹店" target="_blank">地図</a><br>
▪ 🚶龍昌小館・上海厚皮小籠包🥟：<a href="https://www.google.com/maps?q=龍昌小館" target="_blank">地図</a>`
        },
        {
          q: "🚶中華料理🏅",
          a: `
▪ 菜園上海料理店・🏅2025 ミシュラン ビブグルマン：<a href="https://www.google.com/maps?q=菜園上海餐廳" target="_blank">地図</a><br>
▪ 享鴨ローストダック：<a href="https://www.google.com/maps?q=享鴨 烤鴨與中華料理 新竹北大店" target="_blank">地図</a><br>
▪ 西市汕頭館：<a href="https://www.google.com/maps?q=西市汕頭館 北大店" target="_blank">地図</a><br>
▪ 新陶芳（シン タオファン）・ 客家料理：<a href="https://www.google.com/maps?q=新陶芳 東大路" target="_blank">地図</a><br>
▪ 🚕 海底撈火鍋（ハイディーラオ火鍋）：<a href="https://www.google.com/maps?q=海底撈火鍋 新竹" target="_blank">地図</a><br>
▪ 🚕 ノンウェイ ビストロ（弄味小廚）・客家料理・🏅2025 ミシュラン ビブグルマン<a href="https://www.google.com/maps?q=弄味小廚 客家菜系" target="_blank">地図</a><br>
▪ 新橋弄堂：<a href="https://www.google.com/maps?q=新橋弄堂" target="_blank">地図</a>`
        },
        {
          q: "🚶🥩西洋料理",
          a: `
▪ 冪2 La Miette キッチン：<a href="https://www.google.com/maps?q=冪2 La Miette Kitchen" target="_blank">地図</a><br>
▪ Friendy Pizzeria (Friendy ピッツェリア)：<a href="https://www.google.com/maps?q=Friendy Pizzeria" target="_blank">地図</a><br>
▪ 🚕SPASSO Pizza (スパッソピザ)：<a href="https://www.google.com/maps?q=SPASSO" target="_blank">地図</a><br>
▪ 🚕Go eat Tapas Dining BAR・スペイン料理＆バー：<a href="https://www.google.com/maps?q=Go eat Tapas Dining BAR 西班牙餐酒館" target="_blank">地図</a><br>
▪ TABLE JOE キッチン：<a href="https://www.google.com/maps?q=TABLE JOE 喬桌子廚房" target="_blank">地図</a><br>
▪ Stanley (スタンリー)アメリカンステーキハウス🥩：<a href="https://www.google.com/maps?q=史坦利美式牛排 巨城" target="_blank">地図</a><br>
▪ EISEN BISTRO（アイセン・ビストロ）：<a href="https://www.google.com/maps?q=EISEN BISTRO 艾昇小館" target="_blank">地図</a><br>
▪ 金色三麥 新竹巨城店 PARK15：<a href="https://www.google.com/maps?q=金色三麥 新竹巨城店PARK15" target="_blank">地図</a>`
        },
        {
          q: "🚶和食レストラン",
          a: `
▪ 柚子：<a href="https://www.google.com/maps?q=柚子 文化街" target="_blank">地図</a><br>
▪ 皿富器食 minfood：<a href="https://www.google.com/maps?q=皿富器食 minfood" target="_blank">地図</a><br>
▪ 福気キッチン🍣：<a href="https://www.google.com/maps?q=福氣廚房-新竹世界店"_blank">地図</a><br>
▪ 和食川上日本料理🍣：<a href="https://www.google.com/maps?q=和食川上日本料理"_blank">地図</a><br>
▪ 横浜家系ラーメン拉麵家：<a href="https://www.google.com/maps?q=横浜家系ラーメン拉麵家"_blank">地図</a><br>
▪ ラーメン 鶏白湯 ：<a href="https://www.google.com/maps?q=ラーメン 鷄白湯"_blank">地図</a><br>
▪ 麺宮浦島 ：<a href="https://www.google.com/maps?q=麺宮浦島"_blank">地図</a><br>
▪ 🚕 Musha Musha カレー：<a href="https://www.google.com/maps?q=Musha Musha 熟成咖哩 武昌" target="_blank">地図</a><br>
▪ 🚕新竹焼肉 モルディブ本店🍖：<a href="https://www.google.com/maps?q=新竹燒肉 モルディブ馬爾地夫本店" target="_blank">地図</a><br>
▪ 新橋焼肉屋🍖：<a href="https://www.google.com/maps?q=新橋燒肉屋 府後店" target="_blank">地図</a><br>
▪ 私嚐串焼🍢：<a href="https://www.google.com/maps?q=私嚐串燒 中正店" target="_blank">地図</a><br>
▪ 大阪焼肉 燒魂Yakikon🍖：<a href="https://www.google.com/maps?q=大阪燒肉 燒魂Yakikon 新竹市東區"" target="_blank">地図</a>`
        },
  {
          q: "🚶居酒屋🍶",
          a: `
▪ 春菜 小料理：<a href="https://www.google.com/maps?q=春菜 小料理" target="_blank">地図</a><br>
▪ 🚕天狗舞居酒屋：<a href="https://www.google.com/maps?q=天狗舞居酒屋" target="_blank">地図</a><br>
▪ 京町家日式串燒🍢居酒屋：<a href="https://www.google.com/maps?q=京町家日式串燒居酒屋"_blank">地図</a><br>
▪ 隱川居酒屋_いざかや：<a href="https://www.google.com/maps?q=隱川居酒屋_いざかや" target="_blank">地図</a><br>
▪ 乾杯焼肉居酒屋🍖 ビッグシティ店：<a href="https://www.google.com/maps?q=乾杯燒肉居酒屋 新竹巨城店" target="_blank">地図</a>`
        },
        
        {
          q: "🚶ベジタリアン🥗レストラン",
          a: `
▪ 果庭ベジタリアンキッチン：<a href="https://www.google.com/maps?q=果庭蔬食廚房" target="_blank">地図</a><br>
▪  V-Element ベジタリアンレストラン：<a href="https://www.google.com/maps?q=森活原素 V-Element 蔬食餐廳" target="_blank">地図</a><br>
▪ 籽田野菜屋：<a href="https://www.google.com/maps?q=籽田野菜屋" target="_blank">地図</a><br>
▪ 井家：<a href="https://www.google.com/maps?q=井家" target="_blank">地図</a><br>
▪ 井町日式蔬食料理：：<a href="https://www.google.com/maps?q=井町日式蔬食料理 大同店" target="_blank">地図</a><br>
▪ 八二親食：<a href="https://www.google.com/maps?q=八二親食-三民店" target="_blank">地図</a>`
        },
        {
          q: "インド料理＆各国料理",
          a: `
▪ 🚶132官舎ビストロ：<a href="https://www.google.com/maps?q=132官舍/新竹州警務部部長官舍(餐酒館Bistro)" target="_blank">地図</a><br>
▪ 艷麗ポンドック・サニー(シンガポール・マレーシア料理)：<a href="https://www.google.com/maps?q=艷麗Pondok Sunny" target="_blank">地図</a><br>
▪ 蔣好的味道（ジャン ハオ ディ ウェイダオ）台湾・ベトナム小吃：<a href="https://www.google.com/maps?q=蔣好的味道 台越特色小館" target="_blank">地図</a><br>
▪ 🚶青丹扎西（チンダン・ジャシ・チベット料理）：<a href="https://www.google.com/maps?q=青丹扎西 東門市場店" target="_blank">地図</a><br>
▪ エル・ムンド墨多(El Mundo・メキシコ料理)：<a href="https://www.google.com/maps?q=El Mundo墨多" target="_blank">地図</a><br>
▪ スルタン・トルコ料理店：<a href="https://www.google.com/maps?q=蘇丹土耳其廚房" target="_blank">地図</a><br>
▪ 🚶東京純豆腐新竹SOGO店（韓国料理）：<a href="https://www.google.com/maps?q=東京純豆腐Tokyo Sundubu 新竹SOGO店" target="_blank">地図</a><br>
▪ 🚶姜満堂 존맛탱（韓国料理）：<a href="https://www.google.com/maps?q=姜滿堂존맛탱 新竹巨城店" target="_blank">地圖</a><br>
▪ ダダ・インド料理：<a href="https://www.google.com/maps?q=達達印度料理(新竹店)(原 印度小鎮)Burans Indian Kitchen in Hsinchu (Indian Town)" target="_blank">地図</a><br>
▪ 🚶サンシャイン・インディアンレストラン：<a href="https://www.google.com/maps?q=美陽光印度餐廳Sunshine Indian Restaurant Hsinchu" target="_blank">地図</a><br>
▪ CHILLIESINE インド料理レストラン：<a href="https://www.google.com/maps?q=淇里思 新竹店" target="_blank">地図</a><br>
▪ MASインドレストラン：<a href="https://www.google.com/maps?q=MAS India Restaurant 媽媽印度料理" target="_blank">地図</a>`
        },
        {
          q: "牛肉麺🐂🍜🏅",
          a: `
▪ 段純貞牛肉麺：<a href="https://www.google.com/maps?q=段純貞牛肉麵新竹市北區武陵路" target="_blank">地図</a><br>
▪ 🚶九添福（ジウティエンフー）牛肉麺館・🏅2025 ミシュラン ビブグルマン：<a href="https://www.google.com/maps?q=九添福牛肉麵館新竹城隍店" target="_blank">地図</a><br>
▪ 🚶熊川牛肉麺：<a href="https://www.google.com/maps?q=熊川牛肉麵" target="_blank">地図</a><br>
▪ 璽子牛肉麺：<a href="https://www.google.com/maps?q=璽子牛肉麵（博愛店)" target="_blank">地図</a><br>
▪ 貳壹村精緻麺点：<a href="https://www.google.com/maps?q=貳壹村精緻麵點" target="_blank">地図</a>`
        },
        {
          q: "軽食情報",
          a: `
▪ 🚶喜劇終了（バーガー）：<a href="https://www.google.com/maps?q=喜劇收場(漢堡)"_blank"_blank">地図</a><br>
▪ 🚶劇場下アンダーシックスパウンド唐揚げ：<a href="https://www.google.com/maps?q=戲棚下Under Six Pound炸雞" target="_blank">地図</a><br>
▪ 🚶ミックスシェア手作りかき氷：<a href="https://www.google.com/maps?q=覓雪Mixshare手作雪花冰"_blank">地図</a><br>
▪ 白い麦芽餅・茯苓（ぶくりょう）ケーキ：<a href="https://www.google.com/maps?q=白色麥芽餅茯苓糕（米滋食舖）" target="_blank">地図</a><br>
▪ 🚶好豆味冰沙豆花：<a href="https://www.google.com/maps?q=好豆味冰沙豆花 勝利路" target="_blank">地図</a><br>
▪ 山田もち製造所：<a href="https://www.google.com/maps?q=山田麻糬製造所" target="_blank">地図</a><br>
▪ 原夜市鴨肉面：<a href="https://www.google.com/maps?q=原夜市鴨肉麵 中央路" target="_blank">地図</a><br>
▪ 廟口鴨香飯：<a href="https://www.google.com/maps?q=廟口鴨香飯 中山路" target="_blank">地圖</a>`
          
        },
        {
          q: "新竹のお土産🎁",
          a: `
▪ 🚶福源ピーナッツバター：<a href="https://www.google.com/maps?q=福源花生醬 新竹市東區東大路一段" target="_blank">地図</a><br>
▪ 🚶新復珍商行-竹塹餅（チクセンもち）・ビーフン（米粉）：<a href="https://www.google.com/maps?q=新復珍商行"_blank">地図</a><br>
▪ 🚶淵明餅舗-蒸しカステラ：<a href="https://www.google.com/maps?q=淵明餅舖""_blank">地図</a><br>
▪ 進益貢丸：<a href="https://www.google.com/maps?q=進益貢丸新竹市北區北門街"_blank">地図</a><br>
▪ 海瑞貢丸：<a href="https://www.google.com/maps?q=海瑞貢丸新竹西門總店"_blank">地図</a>`
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
