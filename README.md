<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>飯店大廳輪播</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      background: black;
      display: flex;
      flex-direction: column;
    }
    .slideshow-container {
      flex: 1; /* 讓輪播容器填滿除widget外所有高度 */
      display: flex;
      justify-content: center;
      align-items: center;
      overflow: hidden;
      background: black;
    }
    .slides {
      display: none;
      width: 100%;
      height: 100%;
      object-fit: cover;
      background: black;
    }
    .weather-widget-container {
      width: 100%;
      background: black;
    }
  </style>
</head>
<body>

  <div class="slideshow-container">
    <img class="slides" src="Garden.jpg" alt="圖1">
    <img class="slides" src="bf.jpg" alt="圖2">
    <img class="slides" src="SolHotel_M_02.jpg" alt="圖3">
  </div>

  <div class="weather-widget-container">
    <div id="ww_838231a3dcea4" v='1.3' loc='id' a='{"t":"responsive","lang":"ja","sl_lpl":1,"ids":["wl9238"],"font":"Arial","sl_ics":"one_a","sl_sot":"celsius","cl_bkg":"image","cl_font":"#FFFFFF","cl_cloud":"#FFFFFF","cl_persp":"#81D4FA","cl_sun":"#FFC107","cl_moon":"#FFC107","cl_thund":"#FF5722","sl_tof":"3","cl_odd":"#0000000a"}'>
      <a href="https://weatherwidget.org/" id="ww_838231a3dcea4_u" target="_blank">Widget weather</a>
    </div>
    <script async src="https://app3.weatherwidget.org/js/?id=ww_838231a3dcea4"></script>
  </div>

  <script>
    let slideIndex = 0;
    const slides = document.querySelectorAll(".slides");

    function showSlides() {
      slides.forEach(s => s.style.display = "none");

      slideIndex++;
      if (slideIndex > slides.length) { slideIndex = 1; }

      slides[slideIndex - 1].style.display = "block";
      setTimeout(showSlides, 10000); // 每10秒切換
    }

    showSlides();
  </script>

</body>
</html>
