<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>今天天氣真好</title>
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
      background-color: #1a1616; /* 中間黑色 */
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .text-row {
      display: flex;
      gap: 40px; /* 文字之間的間距 */
    }

    .text-row div {
      color: white;
      font-size: 2rem;
      font-family: Arial, sans-serif;
    }
  </style>
</head>
<body>
  <div class="inner-box">
    <div class="text-row">
      <div>今天天氣真好</div>
      <div>今天天氣真好</div>
      <div>今天天氣真好</div>
      <div>今天天氣真好</div>
      <div>今天天氣真好</div>
    </div>
  </div>
</body>
</html>
