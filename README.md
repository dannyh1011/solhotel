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
      align-items: center;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    .lang-selector {
      margin-top: 20px;
    }

    .lang-selector select {
      font-size: 1rem;
      padding: 6px 12px;
      border-radius: 5px;
      border: none;
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
      max-height: 95vh;
      margin: 20px 0;
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

  <!-- 語言選擇器 -->
  <div class="lang-selector">
    <select id="langSelect" onchange="changeLanguage(this.value)">
      <option value="zh">中文</option>
      <option value="en">English</option>
      <option value="jp">日本語</option>
    </select>
  </div>

  <!-- QA 區塊 -->
  <div class="qa-container" id="qa"></div>

  <script>
    const qaData = {
      zh: [
        {
        q: "是否有停車位、充電設施？",
        a: 飯店提供住客免費汽車平面停車場於地下一樓（限高2.2米），您可於入住當日直接進入地下一樓停放，再搭乘電梯至一樓櫃檯登記入住，因車位有限，無法預做保留。<br>
            若館內停車場停滿，您可自行停放至距離飯店步行5分鐘的二個公有停車場，東大路橋下(入口在中央路)或府後停車場，飯店將會支付您的停車費(請於退房11：00前於櫃檯索取停車時數抵用後再行取車)。<br><br>
            ★新春及週末尖峰時段，停車需求量大，如遇等待車位狀況，造成您的不便，敬請見諒。<br>
            ★本館停車場無附設充電設施。
      },
      {
        q: "早餐內容、供應時間？",
        a: ▪ 歐式Buffet，提供中式、西式與日式餐點。<br>
            ▪ 用餐時間 6:30 ~ 10:00，核對房號及用餐人數即可用餐。<br>
            遇年節尖峰用餐時間限時 1 小時。
      },
      {
        q: "是否可提供嬰兒床、床圍？",
        a: 飯店備有嬰兒床、床圍免費租用，如需預訂使用請注意以下事項：<br>
            ▪ 因安全考慮，嬰兒床僅限1歲以下幼兒使用。<br>
            ▪ 一歲以上幼童建議使用床圍，並須入住前安裝。<br>
            ▪ 數量有限，請於訂房同時提前告知。<br>
            ▪ 精緻客房（標準雙人房）無法提供嬰兒床服務。
      },
      {
        q: "是否可提供嬰兒澡盆、奶瓶消毒鍋？",
        a: 本飯店備有嬰兒澡盆(附小板凳 )、奶瓶消毒鍋免費租用。<br>
            因數量不多，如有需要請事先預訂保留。
      },
       {
        q: "浴室內是否有浴缸？",
        a: ▪ 精緻客房（標準雙人房）僅有座式小浴缸。<br>
            ▪ 豪華客房以上房型皆附(單人)標準型浴缸。
      },
      {
        q: "兒童入住加價方式？",
        a: ▪ 1歲以下嬰兒可使用嬰兒床（數量有限，需預訂）<br>
            ▪ 110公分以下免收費<br>
            ▪ 110～140公分加收220元<br>
            ▪ 140公分以上比照成人，建議加床<br>
            ▪ 加床含早餐880元（新春1200元），不含早餐550元（新春1000元）
      },
      {
        q: "成人入住加價方式？",
        a: ▪ 含早餐加床：每人880元（新春1200元）<br>
            僅增加住宿人數：500元（新春800元）<br><br>
            ▪ 不含早餐加床：550元（新春1000元）<br>
            僅增加住宿人數：400元（新春500元）<br>
          ★ 精緻客房（標準雙人房）無法提供加床服務。
      },
      {
        q: "平日價、假日價定義說明？",
        a: ▪ 平日：星期日~星期五<br>▪ 假日：星期六、及特殊節日
      },
      {
        q: "詢問大眾交通、步行、接駁服務？",
        a: ▪ 台鐵新竹站步行約8分鐘抵達飯店（東門國小後門）<br>
            ▪ 高鐵新竹站 → 步行2分鐘過空橋轉乘台鐵(六家站)至新竹站 → 步行8分鐘抵達飯店<br>
            ▪ 本飯店無免費接駁服務
      },
      {
        q: "關於入住時間、行李寄存？",
        a: 入住時間為15:00後，退房時間為翌日11:00前。<br>
            入住前與退房後皆可於櫃檯寄放行李。
      }
      ],
      en: [ {
    q: "Is there parking and EV charging available?",
    a: `Free flat parking is available for hotel guests on B1 (height limit 2.2m). You may park directly upon arrival and take the elevator to the lobby for check-in. Parking is limited and cannot be reserved in advance.<br>
        If full, you can park at two nearby public lots within 5 minutes' walk: under Dongda Rd. Bridge (東大路橋下停車場-entrance on Zhongyang Rd.) or Fu-hou Parking Lot(府後停車場). The hotel will cover the parking fee (please request a parking voucher at the front desk before 11:00 on checkout day).<br><br>
        ★ Parking is in high demand during Chinese New Year and weekends. We apologize for any inconvenience caused by delays.<br>
        ★ No EV charging station available in the hotel.`
  },
  {
    q: "What is the breakfast menu and service time?",
    a: `▪ Buffet with Chinese, Western, and Japanese selections.<br>
        ▪ Served 6:30 ~ 10:00. Please provide your room number and number of guests.<br>
        During peak holiday periods, dining time may be limited to 1 hour.`
  },
  {
    q: "Do you provide baby cots and bed guards?",
    a: `We offer free rental of baby cots and bed guards. Please note:<br>
        ▪ Baby cots are for infants under 1 year old only, for safety reasons.<br>
        ▪ Children over 1 year are advised to use bed guards (must be installed before check-in).<br>
        ▪ Limited availability – please request at time of booking.<br>
        ▪ Baby cots are not available in Standard Double Rooms.`
  },
  {
    q: "Do you offer baby bathtubs and bottle sterilizers?",
    a: `Yes, baby bathtubs (with small stool) and bottle sterilizers are available for free rental.<br>
        Quantities are limited – please reserve in advance.`
  },
  {
    q: "Do bathrooms have bathtubs?",
    a: `▪ Standard Double Rooms: Small seated bathtubs only.<br>
        ▪ Deluxe Rooms and above: Standard single bathtubs included.`
  },
  {
    q: "What are the child surcharges?",
    a: `▪ Infants under 1 may use baby cots (limited, by request).<br>
        ▪ Under 110 cm: Free of charge<br>
        ▪ 110–140 cm: NT$220<br>
        ▪ Over 140 cm: Charged as adult, extra bed recommended<br>
        ▪ Extra bed with breakfast: NT$880 (NT$1200 during Chinese New Year), without breakfast: NT$550 (NT$1000 during CNY)`
  },
  {
    q: "What are the charges for additional adults?",
    a: `▪ With breakfast: NT$880 per person (NT$1200 during CNY)<br>
        Without extra bed: NT$500 (NT$800 during CNY)<br><br>
        ▪ Without breakfast: NT$550 (NT$1000 during CNY)<br>
        Without extra bed: NT$400 (NT$500 during CNY)<br>
        ★ Standard Double Rooms do not support extra beds.`
  },
  {
    q: "What is the definition of weekday and weekend rates?",
    a: `▪ Weekdays: Sunday to Friday<br>▪ Weekends: Saturday and public holidays`
  },
  {
    q: "How to get there by public transportation? Is there shuttle service?",
    a: `▪ 8-minute walk from Hsinchu TRA Station (via Dong Men Elementary School rear gate)<br>
        ▪ From HSR Hsinchu Station → 2-min walk over the skybridge to Liujia TRA Station → transfer to Hsinchu TRA Station → 8-min walk to hotel<br>
        ▪ No shuttle service provided.`
  },
  {
    q: "What are the check-in/out times and luggage storage policy?",
    a: `Check-in: after 15:00; Check-out: before 11:00.<br>
        Luggage storage available at the front desk before check-in and after check-out.`
  }],
      jp: [ {
    q: "駐車場や電気自動車の充電設備はありますか？",
    a: `当ホテルでは、地下1階に高さ制限2.2mの無料平面駐車場を提供しております。ご到着後、直接地下に駐車し、エレベーターで1階フロントへお越しください。駐車スペースには限りがあるため、予約は承っておりません。<br>
        満車の場合は、徒歩5分圏内の公営駐車場（東大路橋下・府後駐車場）をご利用ください。チェックアウト当日の11:00までにフロントで駐車券をご提示いただければ、駐車料金を当ホテルが負担いたします。<br><br>
        ★旧正月や週末など混雑時にはお待たせする場合がございます。あらかじめご了承ください。<br>
        ★館内にはEV充電設備はございません。`
  },
  {
    q: "朝食の内容と提供時間を教えてください。",
    a: `▪ ビュッフェ形式で中華・洋食・和食をご用意しております。<br>
        ▪ 時間：6:30〜10:00、部屋番号と人数を確認後ご利用可能です。<br>
        繁忙期（年末年始など）は利用時間を1時間に制限する場合があります。`
  },
  {
    q: "ベビーベッドやベッドガードの貸し出しはありますか？",
    a: `無料でベビーベッドやベッドガードの貸し出しを行っております。<br>
        ▪ 安全面から、ベビーベッドは1歳未満のお子様に限ります。<br>
        ▪ 1歳以上のお子様にはベッドガードをおすすめします（チェックイン前に設置が必要）。<br>
        ▪ 数に限りがありますので、ご予約時にお申し付けください。<br>
        ▪ スタンダードダブルルームにはベビーベッドを設置できません。`
  },
  {
    q: "ベビーバスや哺乳瓶の消毒器はありますか？",
    a: `ベビーバス（小さな椅子付き）と哺乳瓶消毒器を無料で貸し出しております。<br>
        数に限りがあるため、事前のご予約をおすすめします。`
  },
  {
    q: "バスルームに浴槽はありますか？",
    a: `▪ スタンダードダブルルーム：小型座浴槽のみ<br>
        ▪ デラックスルーム以上：標準サイズの一人用浴槽あり`
  },
  {
    q: "子どもの宿泊料金は？",
    a: `▪ 1歳未満はベビーベッド利用可（要予約）<br>
        ▪ 110cm未満：無料<br>
        ▪ 110～140cm：NT$220<br>
        ▪ 140cm以上：大人料金、エキストラベッド推奨<br>
        ▪ エキストラベッド朝食付き：NT$880（旧正月はNT$1200）<br>
           朝食なし：NT$550（旧正月はNT$1000）`
  },
  {
    q: "大人の追加料金は？",
    a: `▪ 朝食付きエキストラベッド：NT$880（旧正月はNT$1200）<br>
        ベッドなし追加宿泊：NT$500（旧正月はNT$800）<br><br>
        ▪ 朝食なしエキストラベッド：NT$550（旧正月はNT$1000）<br>
        ベッドなし追加宿泊：NT$400（旧正月はNT$500）<br>
        ★ スタンダードダブルルームではエキストラベッドの提供はできません。`
  },
  {
    q: "平日と休日の定義は？",
    a: `▪ 平日：日曜〜金曜<br>▪ 休日：土曜および祝日`
  },
  {
    q: "公共交通機関や送迎サービスについて教えてください。",
    a: `▪ 台鉄・新竹駅から徒歩約8分（東門国小裏門経由）<br>
        ▪ 高鉄・新竹駅 → 徒歩2分で空中通路を通り六家駅 → 台鉄で新竹駅へ → 徒歩8分で当ホテルへ<br>
        ▪ 無料送迎サービスは行っておりません。`
  },
  {
    q: "チェックイン・チェックアウト時間、荷物預かりについて",
    a: `チェックイン：15:00以降、チェックアウト：翌日11:00まで。<br>
        チェックイン前およびチェックアウト後の荷物預かり可能です。`
  }]
    };

    function renderQA(language) {
      const container = document.getElementById('qa');
      container.innerHTML = ''; // 清除原有內容
      qaData[language].forEach((item, index) => {
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

      // 預設展開第一項
      toggleAnswer(0);
    }

    function toggleAnswer(index) {
      const answers = document.querySelectorAll('.answer');
      const arrows = document.querySelectorAll('.arrow');
      answers.forEach((ans, i) => {
        if (i === index) {
          const isOpen = ans.classList.contains('open');
          ans.classList.toggle('open');
          arrows[i].textContent = isOpen ? '▼' : '▲';
        } else {
          ans.classList.remove('open');
          arrows[i].textContent = '▼';
        }
      });
    }

    function changeLanguage(lang) {
      renderQA(lang);
    }

    // 初始語言
    window.onload = () => {
      document.getElementById('langSelect').value = 'zh';
      renderQA('zh');
    };
  </script>
</body>
</html>
