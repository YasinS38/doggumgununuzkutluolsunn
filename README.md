<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>İyi ki Doğdunuz 🎉</title>

<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: radial-gradient(circle at top, #1b1b3a, #050514);
  color: white;
  text-align: center;
  overflow-x: hidden;
}

canvas {
  position: fixed;
  top: 0;
  left: 0;
  z-index: -1;
}

.container {
  padding: 20px;
  animation: fadeIn 1.5s ease;
}

h1 {
  margin-bottom: 30px;
  text-shadow: 0 0 15px #ff6fae;
}

h2 {
  margin: 50px 0 20px;
  animation: glow 1.8s ease-in-out infinite alternate;
}

.gallery {
  display: grid;
  gap: 15px;
}

.gallery.two {
  grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
}

.gallery.four {
  grid-template-columns: repeat(auto-fit, minmax(130px, 1fr));
}

img {
  width: 100%;
  border-radius: 14px;
  cursor: pointer;
  transition: transform 0.35s, box-shadow 0.35s;
}

img:hover {
  transform: scale(1.08);
  box-shadow: 0 0 25px rgba(255,105,180,0.7);
}

.gallery.four img:hover {
  animation: wiggle 0.35s ease-in-out;
}

.big-text {
  font-size: 19px;
  margin-top: 10px;
  line-height: 1.4;
  text-shadow: 0 0 12px #ff82c6;
}

/* Lightbox */
#lightbox {
  position: fixed;
  display: none;
  inset: 0;
  background: rgba(0,0,0,0.92);
  justify-content: center;
  align-items: center;
  z-index: 10;
}

#lightbox img {
  max-width: 90%;
  max-height: 90%;
  border-radius: 14px;
}

/* Footer */
footer {
  position: fixed;
  bottom: 10px;
  left: 12px;
  font-size: 12px;
  opacity: 0.7;
}

/* Animasyonlar */
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

@keyframes glow {
  from { text-shadow: 0 0 5px #ff7eb3; }
  to { text-shadow: 0 0 30px #ff4fa1; }
}

@keyframes wiggle {
  0% { transform: scale(1.08) rotate(0); }
  25% { transform: scale(1.08) rotate(1deg); }
  50% { transform: scale(1.08) rotate(-1deg); }
  75% { transform: scale(1.08) rotate(1deg); }
  100% { transform: scale(1.08) rotate(0); }
}
</style>
</head>

<body>

<canvas id="effects"></canvas>

<div class="container">
  <h1>🎉 İyi ki Doğdunuz 🎉</h1>

  <div class="gallery two">
    <div>
      <img src="cift1.jpg" class="zoom">
      <div class="big-text">
        Doğum gününüz kutlu olsun<br>
        Mutluluklar dilerim 💖
      </div>
    </div>
    <div>
      <img src="cift2.jpg" class="zoom">
      <div class="big-text">
        Doğum gününüz kutlu olsun<br>
        Mutluluklar dilerim 💖
      </div>
    </div>
  </div>

  <h2>📸 Anı Köşesi</h2>

  <div class="gallery four">
    <img src="grup1.jpg" class="zoom">
    <img src="grup2.jpg" class="zoom">
    <img src="grup3.jpg" class="zoom">
    <img src="grup4.jpg" class="zoom">
  </div>
</div>

<footer>Hazırlayan Yasin Şahin</footer>

<div id="lightbox">
  <img id="lightbox-img">
</div>

<script>
// Lightbox
const imgs = document.querySelectorAll('.zoom');
const lightbox = document.getElementById('lightbox');
const lightboxImg = document.getElementById('lightbox-img');

imgs.forEach(img => {
  img.onclick = () => {
    lightbox.style.display = 'flex';
    lightboxImg.src = img.src;
  };
});
lightbox.onclick = () => lightbox.style.display = 'none';

// 🎆 GERÇEK HAVAİ FİŞEK KALPLER
const canvas = document.getElementById("effects");
const ctx = canvas.getContext("2d");

function resize() {
  canvas.width = innerWidth;
  canvas.height = innerHeight;
}
resize();
addEventListener("resize", resize);

let particles = [];
const gravity = 0.12;

function explode(x, y) {
  for (let i = 0; i < 28; i++) {
    const speed = Math.random() * 6 + 3;
    const angle = Math.random() * Math.PI * 2;
    particles.push({
      x,
      y,
      vx: Math.cos(angle) * speed,
      vy: Math.sin(angle) * speed,
      life: 50,
      size: Math.random() * 14 + 12
    });
  }
}

setInterval(() => {
  explode(
    Math.random() * canvas.width,
    Math.random() * canvas.height * 0.5
  );
}, 600);

function animate() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  particles.forEach((p, i) => {
    p.vy += gravity;
    p.x += p.vx;
    p.y += p.vy;
    p.life--;

    ctx.globalAlpha = p.life / 50;
    ctx.font = p.size + "px Arial";
    ctx.fillText("❤️", p.x, p.y);

    if (p.life <= 0) particles.splice(i, 1);
  });

  ctx.globalAlpha = 1;
  requestAnimationFrame(animate);
}
animate();
</script>

</body>
</html>
