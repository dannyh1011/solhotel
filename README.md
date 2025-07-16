# solhotel
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
    .slides {
      display: none;
      width: 100%;
      height: 100%;
      object-fit: cover; 
      background: black;
    }
    iframe.slide-frame {
      display: none;
      width: 100vw;
      height: 100vh;
      border: none;
    }
  </style>
</head>
<body>

  <div class="slideshow-container">
    <img class="slides" src="Garden.jpg" alt="圖1">
    <img class="slides" src="bf.jpg" alt="圖2">
    <img class="slides" src="SolHotel_M_02.jpg" alt="圖3">
    <iframe class="slide-frame" src="https://www.windy.com/zh-TW/-%E9%99%8D%E9%9B%A8%E3%80%81%E9%9B%B7%E6%9A%B4-rain?rain,26.372,138.120,5" title="圖4"></iframe>
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
