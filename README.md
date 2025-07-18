
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>飯店大廳公佈欄輪播</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      width: 100%;
      background: black;
      overflow: hidden;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .slide {
      position: absolute;
      top: 0; left: 0;
      width: 100vw;
      height: 100vh;
      display: none;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      color: white;
      font-size: 48px;
      font-family: Arial, sans-serif;
      text-align: center;
    }
    .slide img {
      max-width: 80%;
      max-height: 80%;
      object-fit: contain;
    }
  </style>
</head>
<body>

  <!-- Slide 1: 圖片公告 -->
  <div class="slide">
    <img src="Garden.jpg" alt="圖1">
    <div>歡迎入住迎曦大飯店</div>
  </div>

  <!-- Slide 2: 純文字公告 -->
  <div class="slide" style="background: #333;">
    <div>早餐供應時間：06:30 - 10:00</div>
  </div>

  <!-- Slide 3: 圖片公告 -->
  <div class="slide">
    <img src="bf.jpg" alt="圖2">
    <div>本館全面禁菸，敬請配合</div>
  </div>

  <script>
    const slides = document.querySelectorAll('.slide');
    let current = 0;

    function showSlide(index) {
      slides.forEach(s => s.style.display = 'none');
      slides[index].style.display = 'flex';
    }

    function nextSlide() {
      current = (current + 1) % slides.length;
      showSlide(current);
    }

    showSlide(current);
    setInterval(nextSlide, 10000); // 每10秒切換
  </script>

</body>
</html>
