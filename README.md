<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>大廳全螢幕天氣顯示</title>
  <style>
    html, body {
      margin: 0;
      padding: 0; 
      width: 100%;
      height: 100%;
      background: #2e2e2e; /* 深灰色背景 */
      display: flex;
      flex-direction: column;
    }
    .widget-section {
      flex: 1;
      display: flex;
      justify-content: center; /* 水平置中 */
      align-items: center;     /* 垂直置中 */
      background: #2e2e2e;
    }
    .widget-section div {
      width: 100%;
      height: 100%;
      max-width: 90vw;
      max-height: 90vh;
    }
  </style>
</head>
<body>
  <!-- 上方：horizontal weather widget -->
  <div class="widget-section">
    <div id="ww_8829fefdbc79c" v="1.3" loc="id" a='{"t":"horizontal","lang":"en","sl_lpl":1,"ids":["wl9238"],"font":"Arial","sl_ics":"one_a","sl_sot":"celsius","cl_bkg":"#2e2e2e","cl_font":"#000000","cl_cloud":"#000000","cl_persp":"#81D4FA","cl_sun":"#FFC107","cl_moon":"#FFC107","cl_thund":"#FF5722"}'>
      <a href="https://weatherwidget.org/" id="ww_8829fefdbc79c_u" target="_blank">Widget weather</a>
    </div>
  </div>

  <!-- 下方：responsive weather widget -->
  <div class="widget-section">
    <div id="ww_c815ce4203541" v="1.3" loc="id" a='{"t":"responsive","lang":"en","sl_lpl":1,"ids":["wl9238"],"font":"Arial","sl_ics":"one_a","sl_sot":"celsius","cl_bkg":"#2e2e2e","cl_font":"#000000","cl_cloud":"#000000","cl_persp":"#81D4FA","cl_sun":"#FFC107","cl_moon":"#FFC107","cl_thund":"#FF5722","cl_odd":"#0000000a"}'>
      <a href="https://weatherwidget.org/" id="ww_c815ce4203541_u" target="_blank">Widget weather</a>
    </div>
  </div>

  <!-- widget scripts -->
  <script async src="https://app3.weatherwidget.org/js/?id=ww_8829fefdbc79c"></script>
  <script async src="https://app3.weatherwidget.org/js/?id=ww_c815ce4203541"></script>
</body>
</html>
