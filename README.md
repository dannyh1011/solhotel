@@ -1,50 +1,53 @@

<html lang="en">
# solhotel
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Two Full Screen Weather Widgets</title>
  <title>飯店大廳輪播</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      width: 100%;
      background: #222;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }
    .widget {
    html, body { margin: 0; padding: 0; height: 100%; background: black; }
    .slideshow-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  background: black;
}
    .slides {
      display: none;
      width: 100%;
      max-width: 1200px;
      flex: 1;
    }
    @media (max-width: 2800px) {
      .widget {
        max-width: 100%;
      }
      height: 100%;
      object-fit: cover;
      background: black;
    }
  </style>
</head>
<body>
  <!-- Widget 1 -->
  <div class="widget">
    <div id="ww_527aa936a9ba0" v='1.3' loc='auto' a='{"t":"horizontal","lang":"en","sl_lpl":1,"ids":["wl9238"],"font":"Arial","sl_ics":"one_a","sl_sot":"celsius","cl_bkg":"image","cl_font":"#FFFFFF","cl_cloud":"#FFFFFF","cl_persp":"#81D4FA","cl_sun":"#FFC107","cl_moon":"#FFC107","cl_thund":"#FF5722"}'>
      <a href="https://weatherwidget.org/" id="ww_527aa936a9ba0_u" target="_blank">Widget weather HTML</a>
    </div>
  </div>

  <!-- Widget 2 -->
  <div class="widget">
    <div id="ww_5c1e90e7842" v='1.3' loc='auto' a='{"t":"responsive","lang":"en","sl_lpl":1,"ids":["wl9238"],"font":"Arial","sl_ics":"one_a","sl_sot":"celsius","cl_bkg":"image","cl_font":"#FFFFFF","cl_cloud":"#FFFFFF","cl_persp":"#81D4FA","cl_sun":"#FFC107","cl_moon":"#FFC107","cl_thund":"#FF5722"}'>
      <a href="https://weatherwidget.org/" id="ww_5c1e90e7842_u" target="_blank">HTML Weather widgets</a>
    </div>
  <div class="slideshow-container">
    <img class="slides" src="r健康訂房" alt="圖1">
    <img class="slides" src="bf.jpg" alt="圖2">
    <img class="slides" src="SolHotel_M_02.jpg" alt="圖3">
  </div>

  <!-- Scripts -->
  <script async src="https://app3.weatherwidget.org/js/?id=ww_527aa936a9ba0"></script>
  <script async src="https://app3.weatherwidget.org/js/?id=ww_5c1e90e7842"></script>
  <script>
    let slideIndex = 0;
    const slides = document.getElementsByClassName("slides");

    function showSlides() {
      for (let i = 0; i < slides.length; i++) {
        slides[i].style.display = "none";
      }
      slideIndex++;
      if (slideIndex > slides.length) { slideIndex = 1; }
      slides[slideIndex - 1].style.display = "block";
      setTimeout(showSlides, 10000); 
    }

    showSlides();
  </script>

</body>
</html>
