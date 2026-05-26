index.html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Mini TikTok</title>

  <link rel="stylesheet" href="style.css">

  <!-- Ícones -->
  <link rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
</head>
<body>

  <div class="app">

    <!-- VIDEO 1 -->
    <div class="video-card active">
      <video src="https://www.w3schools.com/html/mov_bbb.mp4" autoplay muted loop></video>

      <div class="overlay">
        <h2>@usuario1</h2>
        <p>Primeiro vídeo 🔥</p>
      </div>

      <div class="actions">
        <button class="like-btn">
          <i class="fa-solid fa-heart"></i>
          <span>120</span>
        </button>

        <button class="comment-btn">
          <i class="fa-solid fa-comment"></i>
          <span>35</span>
        </button>

        <button class="share-btn">
          <i class="fa-solid fa-share"></i>
          <span>12</span>
        </button>
      </div>
    </div>

    <!-- VIDEO 2 -->
    <div class="video-card">
      <video src="https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4" muted loop></video>

      <div class="overlay">
        <h2>@usuario2</h2>
        <p>Natureza 🌸</p>
      </div>

      <div class="actions">
        <button class="like-btn">
          <i class="fa-solid fa-heart"></i>
          <span>230</span>
        </button>

        <button class="comment-btn">
          <i class="fa-solid fa-comment"></i>
          <span>48</span>
        </button>

        <button class="share-btn">
          <i class="fa-solid fa-share"></i>
          <span>20</span>
        </button>
      </div>
    </div>

    <!-- VIDEO 3 -->
    <div class="video-card">
      <video src="https://www.w3schools.com/html/movie.mp4" muted loop></video>

      <div class="overlay">
        <h2>@usuario3</h2>
        <p>Último vídeo 🚀</p>
      </div>

      <div class="actions">
        <button class="like-btn">
          <i class="fa-solid fa-heart"></i>
          <span>540</span>
        </button>

        <button class="comment-btn">
          <i class="fa-solid fa-comment"></i>
          <span>90</span>
        </button>

        <button class="share-btn">
          <i class="fa-solid fa-share"></i>
          <span>44</span>
        </button>
      </div>
    </div>

    <!-- BOTÕES DE NAVEGAÇÃO -->
    <div class="navigation">
      <button id="prevBtn">
        <i class="fa-solid fa-arrow-left"></i>
      </button>

      <button id="nextBtn">
        <i class="fa-solid fa-arrow-right"></i>
      </button>
    </div>

  </div>

  <script src="script.js"></script>
</body>
</html>
style.css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, sans-serif;
}

body {
  background: #000;
  height: 100vh;
  overflow: hidden;
}

.app {
  width: 100%;
  height: 100vh;
  position: relative;
}

.video-card {
  width: 100%;
  height: 100vh;
  position: absolute;
  display: none;
}

.video-card.active {
  display: block;
}

video {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.overlay {
  position: absolute;
  bottom: 100px;
  left: 20px;
  color: white;
}

.overlay h2 {
  margin-bottom: 10px;
  font-size: 24px;
}

.overlay p {
  font-size: 18px;
}

.actions {
  position: absolute;
  right: 20px;
  bottom: 120px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.actions button {
  background: rgba(0,0,0,0.5);
  border: none;
  color: white;
  padding: 12px;
  border-radius: 50%;
  cursor: pointer;
  font-size: 18px;

  display: flex;
  flex-direction: column;
  align-items: center;

  transition: 0.3s;
}

.actions button:hover {
  transform: scale(1.1);
}

.actions span {
  margin-top: 5px;
  font-size: 14px;
}

.like-active {
  color: red !important;
}

.navigation {
  position: absolute;
  width: 100%;
  top: 50%;
  display: flex;
  justify-content: space-between;
  padding: 0 20px;
  transform: translateY(-50%);
}

.navigation button {
  background: rgba(255,255,255,0.2);
  border: none;
  color: white;
  font-size: 24px;
  padding: 15px;
  border-radius: 50%;
  cursor: pointer;
  transition: 0.3s;
}

.navigation button:hover {
  background: rgba(255,255,255,0.4);
}
script.js
const cards = document.querySelectorAll(".video-card");
const nextBtn = document.getElementById("nextBtn");
const prevBtn = document.getElementById("prevBtn");

let current = 0;

// MOSTRAR VÍDEO
function showVideo(index) {

  cards.forEach((card, i) => {
    const video = card.querySelector("video");

    card.classList.remove("active");
    video.pause();

    if (i === index) {
      card.classList.add("active");
      video.play();
    }
  });
}

// PRÓXIMO
nextBtn.addEventListener("click", () => {
  current++;

  if (current >= cards.length) {
    current = 0;
  }

  showVideo(current);
});

// ANTERIOR
prevBtn.addEventListener("click", () => {
  current--;

  if (current < 0) {
    current = cards.length - 1;
  }

  showVideo(current);
});

// CURTIR
const likeButtons = document.querySelectorAll(".like-btn");

likeButtons.forEach((btn) => {
  btn.addEventListener("click", () => {
    btn.classList.toggle("like-active");
  });
});

// COMENTAR
const commentButtons = document.querySelectorAll(".comment-btn");

commentButtons.forEach((btn) => {
  btn.addEventListener("click", () => {
    alert("Abrir comentários!");
  });
});

// COMPARTILHAR
const shareButtons = document.querySelectorAll(".share-btn");

shareButtons.forEach((btn) => {
  btn.addEventListener("click", () => {

    if (navigator.share) {
      navigator.share({
        title: "Mini TikTok",
        text: "Veja esse vídeo!",
        url: window.location.href
      });
    } else {
      alert("Compartilhamento não suportado no navegador.");
    }

  });
});

// INICIAR
showVideo(current);
