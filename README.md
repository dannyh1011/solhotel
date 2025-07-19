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
      overflow: hidden;
      background: black;
    }
    body::before {
      content: "";
      position: absolute;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: linear-gradient(45deg, red, orange, yellow, green, blue, indigo, violet, red);
      background-size: 400% 400%;
      animation: neon 10s linear infinite;
      opacity: 0.3;
      z-index: 0;
    }
    @keyframes neon {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
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
      font-size: 48px;
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 20px;
      box-sizing: border-box;
      color: white;
      z-index: 1;
    }
    .slide img {
      max-width: 80%;
      max-height: 80%;
      object-fit: contain;
      margin-bottom: 20px;
      filter: drop-shadow(0 0 20px white);
    }
    .marquee {
      position: absolute;
      bottom: 20px;
      width: 100%;
      white-space: nowrap;
      overflow: hidden;
      z-index: 2;
    }
    .marquee span {
      display: inline-block;
      padding-left: 100%;
      animation: marquee 10s linear infinite;
      font-size: 36px;
      background: linear-gradient(45deg, red, orange, yellow, green, blue, purple, red);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      text-shadow: 0 0 10px rgba(255,255,255,0.8);
    }
    @keyframes marquee {
      from { transform: translateX(0%); }
      to { transform: translateX(-100%); }
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
  <div class="slide" style="background: rgba(0,0,0,0.5);">
    <div>早餐供應時間：06:30 - 10:00</div>
  </div>

  <!-- Slide 3: 圖片公告 -->
  <div class="slide">
    <img src="bf.jpg" alt="圖2">
    <div>本館全面禁菸，敬請配合</div>
  </div>

  <!-- 跑馬燈 -->
  <div class="marquee">
    <span>迎曦大飯店歡迎您 ✨ 早餐供應至上午10點 ✨ 本館全面禁菸 ✨</span>
  </div>

  <!-- 台語歌曲背景音樂 -->
  <audio id="bgm" src="your-taiwanese-song.mp3" autoplay loop></audio>

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

    // 自動播放背景音樂（避免 Chrome 阻擋）
    const bgm = document.getElementById('bgm');
    document.addEventListener('click', () => {
      bgm.play();
    });
  </script>

</body>
</html>
