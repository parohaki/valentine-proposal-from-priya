<!DOCTYPE html>
<html lang="en">
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Valentine Proposal 💖</title>

<!-- Google Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&family=Dancing+Script:wght@600;700&display=swap" rel="stylesheet">

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Poppins', sans-serif;
}

body {
  height: 100vh;
  overflow: hidden;
  background: linear-gradient(135deg, #ffd1dc, #ff4f81);
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  position: relative;
  color: white;
}

/* Main Container */
.container {
  position: relative;
  z-index: 2;
  padding: 20px;
}

/* Bouncing Bear */
.bear {
  font-size: 60px;
  animation: bounce 1.5s infinite;
}

@keyframes bounce {
  0%,100% { transform: translateY(0); }
  50% { transform: translateY(-15px); }
}

/* Heading */
h1 {
  font-family: 'Dancing Script', cursive;
  font-size: 40px;
  margin: 20px 0;
}

.subtitle {
  font-style: italic;
  margin-bottom: 20px;
  font-size: 18px;
}

.closing {
  margin-top: 20px;
  font-size: 16px;
}

/* Buttons */
.button-row {
  margin-top: 30px;
  display: flex;
  justify-content: center;
  gap: 40px;
  flex-wrap: wrap;
}

#yesBtn {
  background: linear-gradient(45deg, #ff1e56, #ff4f81);
  border: none;
  color: white;
  padding: 15px 40px;
  font-size: 20px;
  border-radius: 50px;
  cursor: pointer;
  transition: 0.3s;
}

#yesBtn:hover {
  box-shadow: 0 0 20px rgba(255,255,255,0.8);
  transform: scale(1.1);
}

#noBtn {
  background: white;
  color: #ff1e56;
  border: 2px solid #ff1e56;
  padding: 10px 25px;
  font-size: 16px;
  border-radius: 50px;
  cursor: pointer;
  position: relative;
}

/* Floating Hearts */
.heart {
  position: fixed;
  bottom: -20px;
  animation: floatUp linear infinite;
  opacity: 0;
}

@keyframes floatUp {
  0% { transform: translateY(0); opacity: 0; }
  20% { opacity: 1; }
  80% { opacity: 1; }
  100% { transform: translateY(-110vh); opacity: 0; }
}

/* Celebration Screen */
.celebration {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #ff4f81, #ff1e56);
  display: none;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  z-index: 10;
}

.celebration h2 {
  font-size: 60px;
  animation: pulse 1s infinite;
}

@keyframes pulse {
  0%,100% { transform: scale(1); }
  50% { transform: scale(1.2); }
}

.spin {
  font-size: 50px;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  100% { transform: rotate(360deg); }
}

.confetti {
  position: fixed;
  width: 8px;
  height: 8px;
  opacity: 0.9;
}
</style>
</head>

<body>

<div class="container" id="mainContent">
  <div class="bear">🐻</div>
  <h1>Will You Be My Valentine, SHUBHANSHU? 💖</h1>
  <div class="subtitle">I've been gathering courage to ask you this...</div>
  <div class="closing">Every love story is beautiful, but ours is my favourite</div>

  <div class="button-row">
    <button id="yesBtn">Yes ❤️</button>
    <button id="noBtn">No</button>
  </div>
</div>

<div class="celebration" id="celebration">
  <h2>Yayyyy!! 🎉</h2>
  <div class="spin">💖</div>
  <p style="margin-top:20px;font-size:20px;">I knew you'd say yes...</p>
</div>

<script>
const noBtn = document.getElementById("noBtn");
const yesBtn = document.getElementById("yesBtn");
const celebration = document.getElementById("celebration");
const mainContent = document.getElementById("mainContent");

const messages = [
  "Nope, not an option!",
  "Try again!",
  "You sure about that?",
  "Not happening!",
  "Think again!"
];

let msgIndex = 0;

function moveNoButton() {
  const yesRect = yesBtn.getBoundingClientRect();
  const padding = 20;
  let x, y;

  do {
    x = Math.random() * (window.innerWidth - noBtn.offsetWidth);
    y = Math.random() * (window.innerHeight - noBtn.offsetHeight);
  } while (
    x < yesRect.right + padding &&
    x + noBtn.offsetWidth > yesRect.left - padding &&
    y < yesRect.bottom + padding &&
    y + noBtn.offsetHeight > yesRect.top - padding
  );

  noBtn.style.position = "fixed";
  noBtn.style.left = x + "px";
  noBtn.style.top = y + "px";

  noBtn.textContent = messages[msgIndex];
  msgIndex = (msgIndex + 1) % messages.length;
}

noBtn.addEventListener("mouseenter", moveNoButton);
noBtn.addEventListener("click", moveNoButton);
noBtn.addEventListener("touchstart", moveNoButton);

yesBtn.addEventListener("click", () => {
  mainContent.style.display = "none";
  stopHearts();
  celebration.style.display = "flex";
  launchConfetti();
});

/* Floating Hearts */
let heartsInterval;

function createHeart() {
  const heart = document.createElement("div");
  heart.className = "heart";
  heart.textContent = "💖";
  heart.style.left = Math.random() * 100 + "vw";
  heart.style.fontSize = (20 + Math.random() * 30) + "px";
  heart.style.animationDuration = (4 + Math.random() * 4) + "s";
  document.body.appendChild(heart);
  setTimeout(() => heart.remove(), 8000);
}

function startHearts() {
  heartsInterval = setInterval(createHeart, 500);
}

function stopHearts() {
  clearInterval(heartsInterval);
  document.querySelectorAll(".heart").forEach(h => h.remove());
}

startHearts();

/* Confetti */
function launchConfetti() {
  for (let i = 0; i < 120; i++) {
    const confetti = document.createElement("div");
    confetti.className = "confetti";
    confetti.style.backgroundColor = `hsl(${Math.random()*360},100%,50%)`;
    confetti.style.left = Math.random() * 100 + "vw";
    confetti.style.top = "-10px";
    confetti.style.transform = `rotate(${Math.random()*360}deg)`;
    confetti.style.animation = `fall ${3 + Math.random()*2}s linear forwards`;
    document.body.appendChild(confetti);

    const style = document.createElement("style");
    style.innerHTML = `
    @keyframes fall {
      to {
        transform: translateY(100vh) rotate(720deg);
        opacity: 0;
      }
    }`;
    document.head.appendChild(style);

    setTimeout(() => confetti.remove(), 5000);
  }
}
</script>

</body>
</html>
