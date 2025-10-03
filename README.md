
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>I LOVE YOU CANTIKU</title>
  <link href="https://fonts.googleapis.com/css2?family=Pacifico&display=swap" rel="stylesheet">
  <style>
    body {
      margin: 0;
      overflow: hidden;
      background: #000;
      font-family: 'Pacifico', cursive;
      touch-action: none;
    }
    canvas {
      display: block;
    }

    /* Pantalla de carga */
    #loading-screen {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background: #000;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      z-index: 100;
      transition: opacity 0.8s;
    }
    #loading-text {
      font-size: 2.5rem;
      color: white;
      margin-bottom: 30px;
      text-shadow: 0 0 10px #ff00ff;
    }
    .progress-container {
      width: 80%;
      max-width: 500px;
      height: 30px;
      background: rgba(30, 0, 40, 0.6);
      border-radius: 20px;
      overflow: hidden;
      position: relative;
      box-shadow: 0 0 15px rgba(255, 0, 255, 0.5);
      border: 2px solid #ff00ff;
    }
    .progress-bar {
      height: 100%;
      width: 0%;
      background: linear-gradient(90deg, #ff00ff, #00ffff, #ffff00, #ff00aa, #00ffaa, #ff5500);
      background-size: 600% 100%;
      animation: gradientShift 3s linear infinite;
      border-radius: 20px;
    }
    @keyframes gradientShift {
      0% { background-position: 0% 50%; }
      100% { background-position: 600% 50%; }
    }
    .progress-heart {
      position: absolute;
      top: 50%;
      right: 15px;
      transform: translateY(-50%);
      font-size: 1.8rem;
      color: white;
      text-shadow: 0 0 10px #ff00ff;
    }
    #percentage {
      font-size: 2rem;
      margin-top: 20px;
      color: white;
      text-shadow: 0 0 12px #ff00ff;
    }

    /* Menú hamburguesa */
    #menu-btn {
      position: fixed;
      top: 20px;
      left: 20px;
      z-index: 30;
      background: transparent;
      border: none;
      cursor: pointer;
      outline: none;
      padding: 12px;
      border-radius: 50%;
      box-shadow: 0 0 12px #ff00ff, 0 0 20px rgba(255, 0, 255, 0.6);
    }
    #menu-btn span {
      display: block;
      width: 30px;
      height: 4px;
      background: white;
      margin: 6px 0;
      border-radius: 2px;
      box-shadow: 0 0 8px white;
    }

    /* Panel de configuración */
    #config-panel {
      position: fixed;
      top: 0;
      left: -320px;
      width: 300px;
      height: 100vh;
      background: rgba(5, 0, 20, 0.92);
      backdrop-filter: blur(12px);
      color: white;
      padding: 30px 20px;
      z-index: 25;
      transition: left 0.5s cubic-bezier(0.68, -0.55, 0.27, 1.55);
      font-family: 'Pacifico', cursive;
      border-right: 2px solid #ff00ff;
      box-shadow: 0 0 25px rgba(255, 0, 255, 0.7);
      overflow-y: auto;
    }
    #config-panel.active {
      left: 0;
    }
    #close-config {
      position: absolute;
      top: 20px;
      right: 20px;
      background: #ff00ff;
      color: white;
      border: none;
      border-radius: 50%;
      width: 32px;
      height: 32px;
      font-weight: bold;
      cursor: pointer;
      font-family: Arial, sans-serif;
      box-shadow: 0 0 12px #ff00ff;
    }
    #config-panel h2 {
      color: #ff00ff;
      text-align: center;
      margin-top: 0;
      text-shadow: 0 0 12px #ff00ff;
      font-size: 2rem;
    }
    .config-option {
      margin: 18px 0;
      padding: 12px;
      background: rgba(30, 0, 40, 0.7);
      border-radius: 12px;
      border: 1px solid #ff00ff;
      box-shadow: 0 0 10px rgba(255, 0, 255, 0.5);
    }
    .config-option label {
      display: block;
      margin-bottom: 8px;
      color: #ff40ff;
      text-shadow: 0 0 8px #ff40ff;
    }
    .config-option input[type="range"], .config-option input[type="color"] {
      width: 100%;
      margin-top: 5px;
      padding: 6px;
      border-radius: 8px;
      border: 1px solid #ff00ff;
      background: rgba(0,0,0,0.3);
      color: white;
    }
    .image-upload {
      display: flex;
      flex-direction: column;
      gap: 8px;
    }
    .image-upload input {
      display: none;
    }
    .image-upload label {
      padding: 8px;
      background: rgba(100, 0, 150, 0.4);
      border-radius: 8px;
      text-align: center;
      cursor: pointer;
      border: 1px dashed #ff00ff;
      transition: 0.3s;
    }
    .image-upload label:hover {
      background: rgba(150, 0, 200, 0.6);
    }
    .btn-config {
      display: block;
      width: 100%;
      padding: 12px;
      margin-top: 10px;
      background: #ff00ff;
      color: white;
      border: none;
      border-radius: 10px;
      font-family: 'Pacifico', cursive;
      font-size: 1.2rem;
      cursor: pointer;
      box-shadow: 0 0 12px #ff00ff;
    }
    .whatsapp-link {
      display: block;
      text-align: center;
      margin-top: 20px;
      padding: 12px;
      background: #25D366;
      color: white;
      text-decoration: none;
      border-radius: 12px;
      font-family: 'Pacifico', cursive;
      font-size: 1.3rem;
      box-shadow: 0 0 15px #25D366;
    }

    /* Créditos */
    #creditos {
      position: fixed;
      bottom: 15px;
      width: 100%;
      text-align: center;
      font-family: 'Pacifico', cursive;
      font-size: 1.6rem;
      color: white;
      z-index: 12;
      text-shadow: 0 0 10px #ff00ff, 0 0 20px #ff00ff;
    }

    /* Corazones al tocar */
    .heart-explosion {
      position: fixed;
      pointer-events: none;
      z-index: 20;
    }
    .heart-particle {
      position: absolute;
      font-size: 24px;
      opacity: 0;
      animation: explodeHeart 1.2s forwards;
    }
    @keyframes explodeHeart {
      0% {
        transform: translate(0, 0) scale(0.5);
        opacity: 1;
      }
      100% {
        transform: translate(var(--tx), var(--ty)) scale(1.5);
        opacity: 0;
      }
    }
  </style>
</head>
<body>

  <!-- Pantalla de carga -->
  <div id="loading-screen">
    <div id="loading-text">Preparando tu amor... 💖</div>
    <div class="progress-container">
      <div class="progress-bar" id="progress-bar">
        <span class="progress-heart">❤</span>
      </div>
    </div>
    <div id="percentage">0%</div>
  </div>

  <!-- Menú hamburguesa -->
  <button id="menu-btn">
    <span></span>
    <span></span>
    <span></span>
  </button>

  <!-- Panel de configuración -->
  <div id="config-panel">
    <button id="close-config">✕</button>
    <h2>⚙️ Configuración</h2>

    <div class="config-option">
      <label>Velocidad de textos</label>
      <input type="range" id="speed-text" min="0.8" max="5" step="0.1" value="3.0">
    </div>

    <div class="config-option">
      <label>Cantidad de partículas</label>
      <input type="range" id="particle-count" min="300" max="1500" step="50" value="1000">
    </div>

    <div class="config-option">
      <label>Brillo de fotos</label>
      <input type="range" id="photo-glow" min="10" max="70" step="5" value="30">
    </div>

    <div class="config-option">
      <label>
        <input type="checkbox" id="enable-rgb" checked> Modo RGB automático
      </label>
    </div>

    <div class="config-option" id="color-picker-container">
      <label>Color personalizado</label>
      <input type="color" id="custom-color" value="#ff00ff">
    </div>

    <div class="config-option">
      <label>Fotos personales (elige hasta 3)</label>
      <div class="image-upload">
        <input type="file" id="img-upload-1" accept="image/*">
        <label for="img-upload-1">📸 Subir Foto 1</label>
        <input type="file" id="img-upload-2" accept="image/*">
        <label for="img-upload-2">📸 Subir Foto 2</label>
        <input type="file" id="img-upload-3" accept="image/*">
        <label for="img-upload-3">📸 Subir Foto 3</label>
      </div>
    </div>

    <a href="https://wa.me/51930569195" target="_blank" class="whatsapp-link">💬 WhatsApp: +51 930 569 195</a>

    <p style="color: #aaa; font-size: 0.9rem; margin-top: 30px; text-align: center;">
      Desarrollado por AnthZz Berrocal • BerMatMods
    </p>
  </div>

  <canvas id="canvas" style="z-index:1;"></canvas>
  <audio id="bg-music" preload="auto">
    <source src="https://github.com/Baque2005/Organizador/raw/refs/heads/master/PUBLIC%20-%20Make%20You%20Mine%20%20Sub%20espa%C3%B1ol%20  (lyrics).mp3" type="audio/mpeg">
  </audio>

  <div id="creditos">By AnthZz Berrocal BerMatMods</div>

  <script>
    // Configuración global
    let config = {
      textSpeed: 3.0,
      particleCount: 1000,
      photoGlow: 30,
      enableRGB: true,
      customColor: "#ff00ff",
      imageObjects: []
    };

    const COLOR_PALETTE = [
      "#ff00ff", "#00ffff", "#ffff00", "#ff00aa", 
      "#00ffaa", "#ff5500", "#aa00ff", "#00ff55",
      "#ffaa00", "#5500ff", "#ff55aa", "#55ffaa"
    ];
    let currentColorIndex = 0;
    let currentTextColor = config.customColor;
    let currentGlowColor = config.customColor;

    // Menú toggle
    const menuBtn = document.getElementById('menu-btn');
    const configPanel = document.getElementById('config-panel');
    const closeConfig = document.getElementById('close-config');

    menuBtn.onclick = () => configPanel.classList.toggle('active');
    closeConfig.onclick = () => configPanel.classList.remove('active');

    // Aplicar cambios automáticamente
    document.getElementById('speed-text').oninput = (e) => {
      config.textSpeed = parseFloat(e.target.value);
    };
    document.getElementById('particle-count').oninput = (e) => {
      config.particleCount = parseInt(e.target.value);
      if (animacionIniciada) initParticles();
    };
    document.getElementById('photo-glow').oninput = (e) => {
      config.photoGlow = parseInt(e.target.value);
    };
    document.getElementById('enable-rgb').onchange = (e) => {
      config.enableRGB = e.target.checked;
      document.getElementById('color-picker-container').style.display = e.target.checked ? 'none' : 'block';
      if (!config.enableRGB) {
        currentTextColor = config.customColor;
        currentGlowColor = config.customColor;
      }
    };
    document.getElementById('custom-color').oninput = (e) => {
      config.customColor = e.target.value;
      if (!config.enableRGB) {
        currentTextColor = config.customColor;
        currentGlowColor = config.customColor;
      }
    };

    // Carga de imágenes desde galería
    function handleImageUpload(fileInput, index) {
      const file = fileInput.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = (e) => {
          const img = new Image();
          img.src = e.target.result;
          config.imageObjects[index] = img;
          if (animacionIniciada) {
            // Reemplazar en imgDrops si ya está iniciado
            for (let i = 0; i < imgDrops.length; i++) {
              if (imgDrops[i].originalIndex === index) {
                imgDrops[i].img = img;
              }
            }
          }
        };
        reader.readAsDataURL(file);
      }
    }

    document.getElementById('img-upload-1').onchange = () => handleImageUpload(this, 0);
    document.getElementById('img-upload-2').onchange = () => handleImageUpload(this, 1);
    document.getElementById('img-upload-3').onchange = () => handleImageUpload(this, 2);

    // Frases con emojis
    const PHRASES = [
      "❤️ Te amo ❤️", "💖 Te quiero 💖", "✨ Eres mi vida ✨", "🌙 Mi cielo 🌙", "🌟 Eres mi todo 🌟",
      "💫 Eres único/a 💫", "💞 Contigo siempre 💞", "👑 Mi príncipe/princesa 👑", "💗 Mi amor 💗", "🌷 Eres especial 🌷",
      "💝 Solo tú 💝", "😍 Me encantas 😍", "🥰 Te adoro 🥰", "🌹 Mi razón de ser 🌹", "☀️ Eres mi sol ☀️",
      "🌌 Mi eternidad 🌌", "🔐 Nunca sin ti 🔐", "💓 Mi corazón late por ti 💓", "🕊️ Eres mi paz 🕊️",
      "🌍 Mi universo 🌍", "🙏 Te necesito 🙏", "🌠 Eres mi sueño hecho realidad 🌠", "🏡 Eres mi hogar 🏡",
      "🌈 Contigo todo es mejor 🌈", "🎁 Eres mi milagro 🎁", "💍 Amor eterno 💍", "💌 Eres mi todo ❤️",
      "💞 Siempre tuyo/a 💞", "⭐ Mi estrella ⭐", "🌸 Mi flor 🌸", "🔥 Mi pasión 🔥",
      "🦄 Mi arcoíris 🦄", "🌙 Mi luna 🌙", "🌞 Mi sol 🌞", "💎 Mi tesoro 💎"
    ];

    // Explosión de corazones
    function createHeartExplosion(x, y) {
      const explosion = document.createElement('div');
      explosion.className = 'heart-explosion';
      explosion.style.left = x + 'px';
      explosion.style.top = y + 'px';

      for (let i = 0; i < 25; i++) {
        const heart = document.createElement('div');
        heart.className = 'heart-particle';
        heart.innerHTML = '❤';
        heart.style.color = COLOR_PALETTE[Math.floor(Math.random() * COLOR_PALETTE.length)];
        const angle = Math.random() * Math.PI * 2;
        const distance = 50 + Math.random() * 150;
        heart.style.setProperty('--tx', Math.cos(angle) * distance + 'px');
        heart.style.setProperty('--ty', Math.sin(angle) * distance + 'px');
        heart.style.fontSize = (16 + Math.random() * 20) + 'px';
        explosion.appendChild(heart);
      }

      document.body.appendChild(explosion);
      setTimeout(() => document.body.removeChild(explosion), 1200);
    }

    document.body.addEventListener('click', (e) => createHeartExplosion(e.clientX, e.clientY));
    document.body.addEventListener('touchstart', (e) => {
      if (e.touches.length === 1) {
        createHeartExplosion(e.touches[0].clientX, e.touches[0].clientY);
      }
    });

    // Pantalla de carga
    function simulateLoading() {
      const loadingScreen = document.getElementById('loading-screen');
      const progressBar = document.getElementById('progress-bar');
      const percentageEl = document.getElementById('percentage');
      let percent = 0;

      const interval = setInterval(() => {
        percent += Math.random() * 3 + 1;
        if (percent >= 100) {
          percent = 100;
          clearInterval(interval);
          setTimeout(() => {
            loadingScreen.style.opacity = '0';
            setTimeout(() => {
              loadingScreen.style.display = 'none';
              iniciarAnimacionYMusica();
            }, 800);
          }, 500);
        }
        progressBar.style.width = percent + '%';
        percentageEl.textContent = Math.floor(percent) + '%';
      }, 80);
    }

    simulateLoading();

    // Animación principal
    const canvas = document.getElementById("canvas");
    const ctx = canvas.getContext("2d");
    let w, h;
    let animacionIniciada = false;
    let stars = [], hearts = [], texts = [], explosions = [], imgDrops = [];

    function iniciarAnimacionYMusica() {
      if (animacionIniciada) return;
      animacionIniciada = true;
      document.getElementById('bg-music').currentTime = 0;
      document.getElementById('bg-music').play().catch(e => console.log("Audio play failed:", e));

      function resize() {
        w = canvas.width = window.innerWidth;
        h = canvas.height = window.innerHeight;
      }
      window.addEventListener("resize", resize);
      resize();

      const MAX_ACTIVE_TEXTS = 16;
      const SPAWN_INTERVAL = 700;
      let phraseIndex = 0;
      let offsetX = 0, offsetY = 0, zoom = 1;

      // Cambio de color si RGB activado
      if (config.enableRGB) {
        setInterval(() => {
          currentColorIndex = (currentColorIndex + 1) % COLOR_PALETTE.length;
          currentTextColor = COLOR_PALETTE[currentColorIndex];
          currentGlowColor = COLOR_PALETTE[currentColorIndex];
        }, 2000);
      } else {
        currentTextColor = config.customColor;
        currentGlowColor = config.customColor;
      }

      function createStar() {
        return { x: Math.random() * w, y: Math.random() * h, z: Math.random() * 2000, speed: 2 + Math.random() };
      }
      function createHeart() {
        return { x: Math.random() * w, y: Math.random() * h, z: Math.random() * 1600 + 400, speed: 2.5 + Math.random() };
      }
      function spawnTextInOrder(){
        if (texts.length >= MAX_ACTIVE_TEXTS) return;
        const phrase = PHRASES[phraseIndex % PHRASES.length];
        phraseIndex++;
        texts.push({
          text: phrase,
          x: Math.random() * w,
          y: Math.random() * h,
          z: Math.random() * 1600 + 300,
          speed: config.textSpeed + Math.random() * 1.2,
          baseFont: (w < 600 ? 42 : 65),
          glow: 40
        });
      }
      function createImgDrop() {
        let img = null;
        let originalIndex = -1;
        if (config.imageObjects.length > 0) {
          originalIndex = Math.floor(Math.random() * config.imageObjects.length);
          img = config.imageObjects[originalIndex] || new Image();
        } else {
          // Imagen por defecto si no hay ninguna
          img = new Image();
          img.src = "https://i.pinimg.com/1200x/d1/47/50/d147501c6d7854bae28fe00770c5b2d6.jpg";
        }
        return {
          img: img,
          originalIndex: originalIndex,
          x: Math.random() * w,
          y: Math.random() * h,
          z: Math.random() * 1600 + 400,
          speed: 1.8 + Math.random() * 0.8,
          width: (w < 600 ? 140 : 210),
          height: (w < 600 ? 180 : 270)
        };
      }
      function createExplosion() {
        const particles = [];
        const centerX = Math.random() * w;
        const centerY = Math.random() * h;
        for (let i = 0; i < 80; i++) {
          particles.push({
            x: centerX,
            y: centerY,
            vx: (Math.random() - 0.5) * 18,
            vy: (Math.random() - 0.5) * 18,
            life: 1,
            decay: 0.03,
            size: 3 + Math.random() * 8,
            color: currentTextColor
          });
        }
        return { particles, age: 0, maxAge: 90 };
      }

      function initParticles() {
        stars = [];
        hearts = [];
        for (let i = 0; i < config.particleCount; i++) stars.push(createStar());
        for (let i = 0; i < Math.min(80, config.particleCount / 12); i++) hearts.push(createHeart());
      }

      initParticles();
      imgDrops = [];
      for (let i = 0; i < 12; i++) imgDrops.push(createImgDrop());

      function animate() {
        ctx.clearRect(0, 0, w, h);
        const allElements = [];

        stars.forEach(s => {
          s.z -= s.speed;
          if (s.z <= 0) { s.x = Math.random() * w; s.y = Math.random() * h; s.z = 2000; }
          allElements.push({type: 'star', obj: s});
        });

        texts.forEach((t, i) => {
          t.z -= t.speed;
          if (t.z <= 0) { texts.splice(i,1); return; }
          allElements.push({type: 'text', obj: t});
        });

        hearts.forEach(c => {
          c.z -= c.speed;
          if (c.z <= 0) { c.x = Math.random() * w; c.y = Math.random() * h; c.z = 2000; }
          allElements.push({type: 'heart', obj: c});
        });

        imgDrops.forEach(imgDrop => {
          imgDrop.z -= imgDrop.speed;
          if (imgDrop.z <= 0) {
            imgDrop.x = Math.random() * w;
            imgDrop.y = Math.random() * h;
            imgDrop.z = 2000;
            // Reasignar imagen
            if (config.imageObjects.length > 0) {
              const idx = Math.floor(Math.random() * config.imageObjects.length);
              imgDrop.img = config.imageObjects[idx] || imgDrop.img;
              imgDrop.originalIndex = idx;
            }
          }
          allElements.push({type: 'image', obj: imgDrop});
        });

        explosions.forEach((explosion, i) => {
          explosion.age++;
          if (explosion.age > explosion.maxAge) { explosions.splice(i, 1); return; }
          explosion.particles.forEach(p => {
            p.x += p.vx;
            p.y += p.vy;
            p.life -= p.decay;
            p.vx *= 0.98;
            p.vy *= 0.98;
          });
          allElements.push({type: 'explosion', obj: explosion});
        });

        allElements.sort((a, b) => b.obj.z - a.obj.z);

        allElements.forEach(el => {
          const obj = el.obj;
          if (el.type === 'star') {
            const scale = 300 / obj.z * zoom;
            const x = (obj.x - w/2 + offsetX) * scale + w/2;
            const y = (obj.y - h/2 + offsetY) * scale + h/2;
            ctx.fillStyle = currentTextColor;
            ctx.shadowColor = currentGlowColor;
            ctx.shadowBlur = 20;
            ctx.fillRect(x, y, scale*2.5, scale*2.5);
          }
          else if (el.type === 'text') {
            const scale = 250 / obj.z * zoom;
            const x = (obj.x - w/2 + offsetX) * scale + w/2;
            const y = (obj.y - h/2 + offsetY) * scale + h/2;
            ctx.save();
            ctx.translate(x, y);
            ctx.scale(scale, scale);
            ctx.font = `bold ${obj.baseFont}px 'Pacifico'`;
            ctx.fillStyle = currentTextColor;
            ctx.shadowColor = currentGlowColor;
            ctx.shadowBlur = obj.glow;
            ctx.textAlign = "center";
            ctx.fillText(obj.text, 0, 0);
            ctx.restore();
          }
          else if (el.type === 'heart') {
            const scale = 220 / obj.z * zoom;
            const x = (obj.x - w/2 + offsetX) * scale + w/2;
            const y = (obj.y - h/2 + offsetY) * scale + h/2;
            ctx.save();
            ctx.translate(x, y);
            ctx.scale(scale*2.5, scale*2.5);
            ctx.font = "bold 36px 'Pacifico'";
            ctx.fillStyle = currentTextColor;
            ctx.shadowColor = currentGlowColor;
            ctx.shadowBlur = 30;
            ctx.textAlign = "center";
            ctx.fillText("❤", 0, 0);
            ctx.restore();
          }
          else if (el.type === 'image') {
            const scale = 120 / obj.z * zoom;
            const x = (obj.x - w/2 + offsetX) * scale + w/2;
            const y = (obj.y - h/2 + offsetY) * scale + h/2;
            ctx.save();
            ctx.globalAlpha = 0.98;
            ctx.shadowColor = currentGlowColor;
            ctx.shadowBlur = config.photoGlow;
            ctx.drawImage(obj.img, x - obj.width*scale/2, y - obj.height*scale/2, obj.width*scale, obj.height*scale);
            ctx.restore();
          }
          else if (el.type === 'explosion') {
            ctx.save();
            obj.particles.forEach(p => {
              if (p.life > 0) {
                ctx.globalAlpha = p.life;
                ctx.fillStyle = p.color;
                ctx.shadowColor = p.color;
                ctx.shadowBlur = 20;
                ctx.beginPath();
                ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
                ctx.fill();
              }
            });
            ctx.restore();
          }
        });

        requestAnimationFrame(animate);
      }

      animate();
      setInterval(spawnTextInOrder, SPAWN_INTERVAL);
      setInterval(() => explosions.push(createExplosion()), 2500);

      // Controles táctiles
      let startX = 0, startY = 0, lastDist = 0;
      canvas.addEventListener("touchstart", e => {
        if (e.touches.length === 1) {
          const t = e.touches[0];
          startX = t.clientX;
          startY = t.clientY;
        }
      });
      canvas.addEventListener("touchmove", e => {
        e.preventDefault();
        if (e.touches.length === 1) {
          const t = e.touches[0];
          offsetX += (t.clientX - startX) / 3;
          offsetY += (t.clientY - startY) / 3;
          startX = t.clientX;
          startY = t.clientY;
        } else if (e.touches.length === 2) {
          const dx = e.touches[0].clientX - e.touches[1].clientX;
          const dy = e.touches[0].clientY - e.touches[1].clientY;
          const dist = Math.sqrt(dx*dx + dy*dy);
          if (lastDist) {
            zoom *= dist / lastDist;
            zoom = Math.min(Math.max(0.5, zoom), 3);
          }
          lastDist = dist;
        }
      });
      canvas.addEventListener("touchend", () => lastDist = 0);
    }
  </script>
</body>
</html>
