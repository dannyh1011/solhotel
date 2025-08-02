<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <title>新竹站台鐵即時列車動態</title>
  <meta http-equiv="refresh" content="300" />
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      width: 100%;
      background: #000;
      overflow: hidden;
    }

    iframe {
      border: none;
      width: 100vw;
      height: 100vh;
      display: block;
    }

    /* 🔽 新增：隱藏可能的標題與紅框容器 */
    #solhotel,
    .solhotel,
    header,
    .header,
    .top-bar,
    .branding,
    .red-border,
    .logo-container,
    h1,
    h2 {
      display: none !important;
    }
  </style>
</head>
<body>
  <iframe 
    src="https://railway.chienwen.net/taiwan/station/TRA-1210-%E6%96%B0%E7%AB%B9/live" 
    title="新竹站台鐵即時列車動態">
  </iframe>
</body>
</html>
