<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="style.css" />
    <link
      rel="stylesheet"
      href="https://fonts.googleapis.com/css2?family=Manrope:wght@400;500;700&display=swap"
    />
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.1/css/all.min.css"
    />
    <script
      src="https://kit.fontawesome.com/5f0f2ef141.js"
      crossorigin="anonymous"
    ></script>
    <style>
      body {
        margin: 0;
        padding: 0;
        width: 100vw;
        height: 100vh;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        background-color: #f4f4f4; /* Color de fondo mientras carga */
        background-image: url("https://cdn.glitch.global/08eee73d-920d-48eb-874a-8f48b02f0313/Frame%2024%20(10).png?v=1739202041894");
        background-position: top;
        background-size: cover;
        background-repeat: no-repeat;
      }

      header {
        background-image: url("https://cdn.glitch.global/b69b65d8-5a31-4a84-8cd6-0ce3869d6186/Frame%2057.png?v=1726869980392");
        background-size: cover;
        color: #ffffff;
        padding: 1px;
        text-align: center;
        width: 100%;
        font-size: 12px;
        border-bottom-right-radius: 40px;
        border-bottom-left-radius: 40px;
        z-index: 1;
        position: fixed;
        top: 0;
        display: flex;
        justify-content: space-evenly;
        align-items: center;
        box-shadow: 0 5px 10px rgba(0, 0, 0, 0.3); /* Efecto de sombra en la parte inferior */
      }

      .main-buttons {
        display: flex;
        margin: 10px;
      }

      .button-left {
        margin-right: auto;
      }

      .button-right {
        margin-left: auto;
      }

      img {
        width: 60%;
        max-width: 150px;
        height: auto;
        object-fit: contain;
        margin-right: 10px;
        margin-left: 10px;
        display: block;
      }

      model-viewer {
        width: 100%;
        height: 70vh;
        background-color: transparent;
        position: relative;
        margin-top: 0px;
      }

      .button-container {
        position: absolute;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        height: 100%;
        top: 0;
        left: 0;
        padding: 20px;
        box-sizing: border-box;
        pointer-events: none;
        z-index: 2;
      }

      .button-container-right {
        position: absolute;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        height: 100%;
        top: 0;
        right: 0;
        padding: 20px;
        box-sizing: border-box;
        pointer-events: none;
        z-index: 2;
      }

      .button {
        width: 60px;
        height: 60px;
        background-color: #6affb9;
        border-radius: 50%;
        margin: 15px 0;
        cursor: pointer;
        pointer-events: all;
        display: flex;
        align-items: center;
        justify-content: center;
        text-decoration: none;
        color: #141436;
        box-sizing: border-box;
      }

      .button i {
        font-size: 24px;
        color: #141436;
      }

      .progress-bar {
        display: block;
        width: 33%;
        height: 10%;
        max-height: 2%;
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate3d(-50%, -50%, 0);
        border-radius: 25px;
        box-shadow: 0px 3px 10px 3px rgba(0, 0, 0, 0.5),
          0px 0px 5px 1px rgba(0, 0, 0, 0.6);
        border: 1px solid rgba(255, 255, 255, 0.9);
      }

      .progress-bar.hide {
        visibility: hidden;
        transition: visibility 0.3s;
      }

      .update-bar {
        background-color: rgba(20, 20, 20, 0.9);
        width: 0%;
        height: 100%;
        border-radius: 25px;
        float: left;
        transition: width 0.3s;
      }

      @keyframes circle {
        from {
          transform: translateX(-50%) rotate(0deg) translateX(50px) rotate(0deg);
        }
        to {
          transform: translateX(-50%) rotate(360deg) translateX(50px)
            rotate(-360deg);
        }
      }

      @keyframes elongate {
        from {
          transform: translateX(100px);
        }
        to {
          transform: translateX(-100px);
        }
      }

      model-viewer > #ar-prompt {
        position: absolute;
        left: 50%;
        bottom: 175px;
        animation: elongate 2s infinite ease-in-out alternate;
        display: none;
      }

      model-viewer[ar-status="session-started"] > #ar-prompt {
        display: block;
      }

      model-viewer > #ar-prompt > img {
        animation: circle 4s linear infinite;
      }

      footer {
        background-image: url(https://cdn.glitch.global/b69b65d8-5a31-4a84-8cd6-0ce3869d6186/Frame%2057.png?v=1726869980392);
        background-size: cover;
        width: 100%;
        font-size: 12px;
        color: #ffffff;
        text-align: center;
        bottom: 0px;
        border-top-right-radius: 40px;
        border-top-left-radius: 40px;
        font-family: arial;
        position: fixed;
        box-shadow: 0 -5px 10px rgba(0, 0, 0, 0.3); /* Efecto de sombra en la parte superior */
      }

      /* Estilos adicionales según sea necesario */

      /* Estilo para el popup 1 */
      .popup1 {
        display: none;
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: white;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
        z-index: 3;
        width: 60%;
        height: 60%;
      }

      /* Estilo para el popup 2 */
      .popup2 {
        display: none;
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: white;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
        z-index: 3;
        width: 60%;
        height: 60%;
        text-align: center;
      }

      .popup img {
        max-width: 100%;
        height: auto;
        max-height: 80vh; /* Establecer una altura máxima si es necesario */
        display: inline-block;
        vertical-align: middle;
        margin: auto;
      }

      .overlay {
        display: none;
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.5);
        z-index: 2;
      }

      .oculto {
        display: none;
      }
    </style>

    <title>Tag virtual Juan José Semaan</title>
  </head>

  <body>
    <header>
      <div class="main-buttons">
        <button
          style="background-color: #6affb9"
          class="button button-left"
          onclick="window.location.href='https://wa.me/+573152591115'"
        >
          <i class="fa-brands fa-whatsapp"></i>
        </button>

        <img
          src="https://cdn.glitch.global/08eee73d-920d-48eb-874a-8f48b02f0313/image%201%20(3).png?v=1738171123190"
          alt="Descripción de la imagen"
        />

        <button
          style="background-color: #6affb9"
          class="button button-right"
          onclick="window.location.href='tel:+573152591115'"
        >
          <i class="fas fa-phone"></i>
        </button>
      </div>
    </header>

    <div class="main-buttons">
      <!-- Agrega más botones según sea necesario -->
    </div>

    <model-viewer
      auto-rotate
      src=""
      autoplay
      ar-modes="scene-viewer webxr quick-look"
      auto-rotate-delay="0"
      rotation-per-second="1deg"
      interaction-prompt="none"
      exposure="0.6"
      shadow-softness="0.5"
      camera-orbit="0 90deg 3m"
      min-camera-orbit="0 90deg 1.5m"
      camera-controls
      style="max-height: 90vh; max-width: 90vw"
    >
      <div class="botones">
        <div class="button-container">
          <a class="button" href="https://www.behance.net/juanjosesemaan">
            <i class="fa-brands fa-behance"></i>
          </a>
          <a class="button" href="https://semaan111.wixsite.com/my-site">
            <i class="fa-solid fa-globe"></i>
          </a>
          <a
            class="button"
            href="https://cdn.glitch.global/08eee73d-920d-48eb-874a-8f48b02f0313/Acta%20de%20grado%20Especializaci%C3%B3n.pdf?v=1738166960957"
          >
            <i class="fa-solid fa-graduation-cap"></i>
          </a>
        </div>

        <div class="button-container-right">
          <a
            class="button"
            href="https://www.linkedin.com/in/juanjosesemaanmolina-productdesigner/"
          >
            <i class="fa-brands fa-linkedin"></i>
          </a>

          <a class="button" href="mailto:	semaan111@gmail.com">
            <i class="fas fa-envelope"></i>
          </a>
          <a class="button" href="https://www.instagram.com/semaan.111">
            <i class="fa-brands fa-instagram"></i>
          </a>
        </div>

        <div class="progress-bar hide" slot="progress-bar">
          <div class="update-bar"></div>
        </div>
      </div>

      <div id="ar-prompt">
        <img
          src="https://cdn.glitch.global/830ab8b2-f7c8-42f2-a062-abfa2deb8750/ar_hand_prompt.png?v=1661980926699"
        />
      </div>
    </model-viewer>

    <div class="overlay" id="overlay"></div>

    <script src="script.js"></script>

    <!-- Loads <model-viewer> for browsers: -->
    <script
      type="module"
      src="https://unpkg.com/@google/model-viewer/dist/model-viewer.min.js"
    ></script>

    <audio id="miAudio" class="oculto" controls>
      <source
        src="https://cdn.glitch.global/08eee73d-920d-48eb-874a-8f48b02f0313/WhatsApp-Ptt-2025-01-29-at-11-VEED%20(1).mp3?v=1738169255342"
        type="audio/mp3"
      />
      Tu navegador no soporta la etiqueta de audio.
    </audio>

    <button
      class="btn-audio"
      onclick="document.getElementById('miAudio').play()"
    >
      ¡Escúchame aquí!
      <i class="fa-solid fa-volume-high"></i>
    </button>

    <style>
      @import url("https://fonts.googleapis.com/css2?family=Inter:wght@900&display=swap");

      .btn-audio {
        font-family: "Poppins", sans-serif;
        font-weight: 900;
        background-color: #222222;
        color: #6affb9;
        padding: 10px 20px;
        border: none;
        border-radius: 100px;
        cursor: pointer;
        font-size: 18px;
        text-transform: uppercase;
        letter-spacing: 1px;
        transition: background-color 0.3s ease;

        transform: translatey(-400%); /* Centrado horizontal */
      }

      .btn-audio:hover {
        background-color: #555;
      }

      .btn-audio:active {
        background-color: #111;
      }
    </style>

    <footer>
      <p style="font-family: 'Poppins', sans-serif; font-weight: 900">
        Juan José Semaan / Product Designer
      </p>
    </footer>
  </body>
</html>
