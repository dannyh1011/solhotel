# solhotel
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>飯店大廳輪播</title>
  <style>
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
      height: 100%;
      object-fit: cover;
      background: black;
    }
  </style>
</head>
<body>

  <div class="slideshow-container">
    <img class="slides" src="Garden.jpg" alt="圖1">
    <img class="slides" src="bf.jpg" alt="圖2">
  </div>

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
      setTimeout(showSlides, 10000); // 每5秒切換
    }

    showSlides();
  </script>

</body>
</html>
