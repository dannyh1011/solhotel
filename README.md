
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
    }
    .slideshow-container {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 100vw;
      height: 100vh;
      overflow: hidden;
      background: black;
    }
    .slides, iframe.slide-frame {
      display: none;
      width: 100%;
      height: 100%;
      object-fit: cover;
      background: black;
      border: none;
    }
  </style>
</head>
<body>

  <div class="slideshow-container">
    <img class="slides" src="Garden.jpg" alt="圖1">
    <img class="slides" src="bf.jpg" alt="圖2">
    <a class="weatherwidget-io" href="https://forecast7.com/ja/24d81120d97/hsinchu-city/" data-label_1="HSINCHU CITY" data-label_2="WEATHER" data-font="ヒラギノ角ゴ Pro W3" data-icons="Climacons" data-days="5" data-theme="weather_one" >HSINCHU CITY WEATHER</a>
<script>
!function(d,s,id){var js,fjs=d.getElementsByTagName(s)[0];if(!d.getElementById(id)){js=d.createElement(s);js.id=id;js.src='https://weatherwidget.io/js/widget.min.js';fjs.parentNode.insertBefore(js,fjs);}}(document,'script','weatherwidget-io-js');
</script>
    <img class="slides" src="SolHotel_M_02.jpg" alt="圖3">
    <!--Begin Weather Widget -->
    <iframe class="slide-frame"
            src="https://taiwanweather.org/widget/embed/hsinchu/hsinchu-county?style=1&day=3&td=%23003870&ntd=%23ff0000&mvb=%23c0161f&mv=%23ff0000&mdk=%230cb07f&htd=true"
            id="widgeturl"
            scrolling="no"
            frameborder="0"
            allowtransparency="true">
    </iframe>
    <!-- End Widget -->
  </div>

  <script>
    let slideIndex = 0;
    const slides = document.querySelectorAll(".slides, .slide-frame");

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
