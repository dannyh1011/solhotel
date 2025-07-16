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
    <iframe class="slide-frame"
        src="https://www.cwa.gov.tw/V8/C/SimplePlugin.html?style=W2&cid=10018"
        width="100%" height="100%" frameborder="0" scrolling="no">
</iframe>

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
