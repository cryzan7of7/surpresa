<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <title>Surpresa do Dia das Mães</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100vh;
      font-family: 'Georgia', serif;
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: black;
      color: white;
      overflow: hidden;
      flex-direction: column;
    }

    .login, .tela-preta, .conteudo {
      display: none;
      flex-direction: column;
      align-items: center;
    }

    .login input, .login select, .login button {
      margin: 10px;
      padding: 10px;
      font-size: 1em;
      border-radius: 10px;
      border: none;
    }

    .login button {
      background-color: #ec407a;
      color: white;
      cursor: pointer;
    }

    .tela-preta button {
      margin-top: 20px;
      padding: 12px 25px;
      font-size: 1.1em;
      background-color: #ffffff;
      color: black;
      border: none;
      border-radius: 30px;
      cursor: pointer;
    }

    .revelado {
      background: radial-gradient(circle, #fff0f6, #f8bbd0);
      color: #880e4f;
    }

    h1 {
      font-size: 3em;
      margin-bottom: 20px;
      animation: zoomIn 2s ease-out;
      display: none;
    }

    #mensagem {
      font-size: 1.4em;
      width: 60%;
      text-align: center;
      white-space: pre-line;
      display: none;
      animation: fadeIn 2s ease forwards;
    }

    .flor {
      position: absolute;
      animation: flutuar 12s linear infinite;
      opacity: 0.8;
      pointer-events: none;
    }

    @keyframes flutuar {
      0% {
        transform: translateY(-100px) rotate(0deg);
      }
      100% {
        transform: translateY(110vh) rotate(360deg);
      }
    }

    @keyframes fadeIn {
      from {opacity: 0;}
      to {opacity: 1;}
    }

    @keyframes zoomIn {
      from {transform: scale(0.7); opacity: 0;}
      to {transform: scale(1); opacity: 1;}
    }
  </style>
</head>
<body>

  <!-- TELA DE LOGIN -->
  <div class="login" id="login">
    <h2>Login Especial</h2>
    <input type="text" id="nome" placeholder="Digite seu nome" />
    <label for="nivel">Nível de chatice:</label>
   <select id="nivel">
  <script>
    for (let i = 1; i <= 10; i++) {
      document.write(`<option value="${i}">${i}</option>`);
    }
  </script>
</select>
    <button onclick="verificarLogin()">Entrar</button>
    <p id="erro" style="color:red;"></p>
  </div>

  <!-- TELA PRETA -->
  <div class="tela-preta" id="intro">
    <h2>Clique para revelar uma surpresa especial 💝</h2>
    <button onclick="revelar()">Mostrar</button>
  </div>

  <!-- CONTEÚDO PRINCIPAL -->
  <div class="conteudo" id="principal">
    <h1 id="titulo">🌷 Para a Melhor Mãe do Mundo 🌷</h1>
    <div id="mensagem"></div>
  </div>

  <audio id="musica" loop>
    <source src="https://www.bensound.com/bensound-music/bensound-love.mp3" type="audio/mpeg">
  </audio>

  <script>
    const mensagem = `Mãe, Feliz seu dia, amo ser seu filho.
mesmo com toda sua chatisse, é a melhor mãe que alguém pode ter

Cada passo meu leva um pouco de você:
sua força, seu jeito, seu olhar e até suas estranhices kkkk.

Neste dia especial, só posso dizer:
Obrigado por ser minha luz eterna.

Feliz Dia das Mães!
TE AMO MUITO 💖`;

    // Começa com login
    document.getElementById("login").style.display = "flex";

    function verificarLogin() {
      const nome = document.getElementById("nome").value.trim().toLowerCase();
      const nivel = document.getElementById("nivel").value;
      if (nome === "adriana" && nivel === "10") {
        document.getElementById("login").style.display = "none";
        document.getElementById("intro").style.display = "flex";
      } else {
        document.getElementById("erro").innerText = "Nome ou nível incorretos! 😅";
      }
    }

    function revelar() {
      document.getElementById("intro").style.display = "none";
      document.body.classList.add("revelado");
      document.getElementById("principal").style.display = "flex";

      setTimeout(() => {
        document.getElementById("titulo").style.display = "block";
        document.getElementById("mensagem").style.display = "block";
        escreverMensagem();
        document.getElementById("musica").play().catch(() => alert("Clique para ativar o áudio"));
        iniciarFlores();
      }, 1000);
    }

    let i = 0;
    function escreverMensagem() {
      const divMensagem = document.getElementById("mensagem");
      if (i < mensagem.length) {
        divMensagem.innerHTML += mensagem.charAt(i);
        i++;
        setTimeout(escreverMensagem, 50);
      }
    }

    function iniciarFlores() {
      const flores = ["🌸", "🌼", "🌷", "💮"];
      for (let j = 0; j < 30; j++) {
        const flor = document.createElement("div");
        flor.className = "flor";
        flor.innerText = flores[Math.floor(Math.random() * flores.length)];
        flor.style.left = Math.random() * 100 + "vw";
        flor.style.fontSize = Math.random() * 24 + 16 + "px";
        flor.style.top = -Math.random() * 500 + "px";
        flor.style.animationDuration = (Math.random() * 10 + 10) + "s";
        document.body.appendChild(flor);
      }
    }
  </script>

</body>
</html>
