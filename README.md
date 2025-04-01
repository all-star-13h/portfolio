const canvas = document.createElement("canvas");
const ctx = canvas.getContext("2d");
document.body.appendChild(canvas);
canvas.style.position = "fixed";
canvas.style.top = "0";
canvas.style.left = "0";
canvas.style.width = "100vw";
canvas.style.height = "100vh";
canvas.style.zIndex = "-1";
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

const columns = Math.floor(canvas.width / 20);
const drops = Array(columns).fill(1);
const fontSize = 20;
const matrixChars = "ABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890".split("");

function draw() {
  ctx.fillStyle = "rgba(0, 0, 0, 0.1)";
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  ctx.fillStyle = "#0F0";
  ctx.font = `${fontSize}px monospace`;

  for (let i = 0; i < drops.length; i++) {
    const text = matrixChars[Math.floor(Math.random() * matrixChars.length)];
    ctx.fillText(text, i * fontSize, drops[i] * fontSize);
    
    if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
      drops[i] = 0;
    }
    drops[i]++;
  }
  requestAnimationFrame(draw);
}

draw();

window.addEventListener("resize", () => {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
});
