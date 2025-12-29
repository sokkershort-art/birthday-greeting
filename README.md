<!DOCTYPE html>
<html>
<head>
  <title>Happy Birthday Sakshi</title>
  <style>
    body {
      margin: 0;
      background: #ffc0cb;
      font-family: "Comic Sans MS", cursive;
      height: 100vh;
      overflow: hidden;
      cursor: pointer;
      display: flex;
      justify-content: center;
      align-items: center;
      text-align: center;
    }

    .slide {
      display: none;
      animation: fadeIn 1s ease;
      z-index: 1;
    }

    h1, h2, h3, p {
      margin: 10px 0;
    }

    .hint {
      position: absolute;
      bottom: 20px;
      font-size: 14px;
      color: #800040;
      opacity: 0.7;
      z-index: 5;
    }

    /* ==== Slide Fade ==== */
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(30px);}
      to { opacity: 1; transform: translateY(0);}
    }

    /* ==== 3D Cube ==== */
    .scene {
      width: 150px;
      height: 150px;
      perspective: 600px;
      margin: auto;
      z-index: 2;
    }

    .cube {
      width: 100%;
      height: 100%;
      position: relative;
      transform-style: preserve-3d;
      transition: transform 0.6s ease;
    }

    .face {
      position: absolute;
      width: 150px;
      height: 150px;
      background: #ff69b4;
      border: 2px solid #cc3366;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 38px;
      box-shadow: inset 0 0 20px rgba(255,255,255,0.6);
    }

    .front  { transform: translateZ(75px); }
    .back   { transform: rotateY(180deg) translateZ(75px); }
    .right  { transform: rotateY(90deg)  translateZ(75px); }
    .left   { transform: rotateY(-90deg) translateZ(75px); }
    .top    { transform: rotateX(90deg)  translateZ(75px); }
    .bottom { transform: rotateX(-90deg) translateZ(75px); }
    .front::after { content: "🙂"; }

    /* ==== Falling Text ==== */
    .falling-text {
      position: absolute;
      top: -50px;
      font-size: 18px;
      font-weight: bold;
      color: #660033;
      animation: fall linear;
      white-space: nowrap;
      opacity: 0.9;
      pointer-events: none;
      z-index: 0;
    }

    @keyframes fall {
      to {
        transform: translateY(110vh);
        opacity: 0;
      }
    }

    /* ==== Typing Effect ==== */
    @keyframes typing {
      from { width: 0; }
      to { width: 100%; }
    }

    .typed {
      display: inline-block;
      overflow: hidden;
      border-right: 2px solid #660033;
      white-space: nowrap;
      animation: typing 3s steps(30, end) forwards;
    }
  </style>
</head>
<body onclick="nextSlide()">

  <!-- Slide 1 -->
  <div id="slide1" class="slide">
    <h2 class="typed">✨ Welcome ✨</h2>
    <p class="typed">A special greeting from <b>Your Krishna</b></p>
  </div>

  <!-- Slide 2 -->
  <div id="slide2" class="slide">
    <h2 class="typed">🎂 Happy Birthday Sakshi 🎂</h2>
  </div>

  <!-- Slide 3 -->
  <div id="slide3" class="slide">
    <p class="typed">
      Happy Birthday!<br><br>
      Honestly, I’m really glad to have you in my life.<br><br>
      Hope this year treats you kindly<br>
      and keeps you smiling 😊
    </p>
    <p class="typed"><br>— Your Krishna 💗</p>
  </div>

  <!-- Final Slide -->
  <div id="slide4" class="slide">
    <div class="scene">
      <div class="cube" id="cube" onclick="rotateCube(event)">
        <div class="face front"></div>
        <div class="face back"></div>
        <div class="face right"></div>
        <div class="face left"></div>
        <div class="face top"></div>
        <div class="face bottom"></div>
      </div>
    </div>
    <p><br>Tap the cube 🙂</p>
  </div>

  <div class="hint">👉 Tap / Click to continue</div>

  <script>
    let slides = document.getElementsByClassName("slide");
    let index = 0;
    slides[index].style.display = "block";

    function nextSlide() {
      if (index < slides.length - 1) {
        slides[index].style.display = "none";
        index++;
        slides[index].style.display = "block";

        if (index === 3) startFallingText();
      }
    }

    // Cube rotate
    let rotateX = 0, rotateY = 0;
    function rotateCube(e){
      e.stopPropagation();
      rotateX += Math.floor(Math.random() * 90)+45;
      rotateY += Math.floor(Math.random() * 90)+45;
      document.getElementById("cube").style.transform =
        `rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
    }

    // Falling text effect
    function startFallingText(){
      let messages = [
        "Happy Birthday! 💕",
        "Keep Smiling 😊",
        "You are Special 🌸",
        "Best Wishes 🎉",
        "Love & Happiness 💖"
      ];
      setInterval(()=>{
        let text = document.createElement("div");
        text.className = "falling-text";
        text.innerText = messages[Math.floor(Math.random()*messages.length)];
        text.style.left = Math.random()*90 + "vw";
        text.style.animationDuration = (Math.random()*3 + 3) + "s";
        document.body.appendChild(text);
        setTimeout(()=>text.remove(),4000);
      },500);
    }
  </script>

</body>
</html>
