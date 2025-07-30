<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>背景底圖</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      background-color: #a67c52; /* 外框棕色 */
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .inner-box {
      width: 90%;
      height: 90%;
      background-color: #1a1616; /* 內部黑色 */
      box-shadow: inset 0 0 0 0; /* 無陰影 */
    }
  </style>
</head>
<body>
  <div class="inner-box">
    <!-- 可放置天氣 widget 或其他內容 -->
  </div>
</body>
</html>
🎨 色碼參考（從圖片擷取）：
邊框棕色（外圍）：#a67c52

內部黑色：#1a1616

