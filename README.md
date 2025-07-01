# casino-tragamonedas-sanma
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Tragamonedas Sanma</title>
  <style>
    body {
      background: #0a0a0a;
      color: #fff;
      text-align: center;
      font-family: Arial, sans-serif;
      padding: 30px;
    }

    h1 {
      font-size: 60px;
      color: gold;
      margin-bottom: 20px;
    }

    #maquina {
      background: #004d4d;
      border: 15px solid gold;
      border-radius: 30px;
      width: 90vw;
      max-width: 500px;
      margin: auto;
      padding: 30px;
      box-shadow: 0 0 40px #ffaa00;
    }

    #slots {
      display: flex;
      justify-content: space-around;
      font-size: 120px;
      background: #fff;
      border-radius: 20px;
      padding: 30px;
      color: black;
      margin-bottom: 30px;
      height: 160px;
      align-items: center;
      overflow: hidden;
    }

    .rodillo {
      animation: girar 1s linear;
    }

    @keyframes girar {
      0% { transform: rotateX(0deg); }
      100% { transform: rotateX(1080deg); } /* 3 vueltas rápidas */
    }

    button {
      background: gold;
      border: none;
      font-size: 40px;
      padding: 20px 50px;
      border-radius: 20px;
      cursor: pointer;
    }

    #mensaje {
      margin-top: 30px;
      font-size: 36px;
    }

    #reflexion {
      margin-top: 50px;
      background: #ffcccc;
      color: #8b0000;
      font-size: 40px;
      padding: 30px;
      border-radius: 20px;
      display: none;
    }
  </style>
</head>
<body>

  <h1>🎰 Casino Virtual Sanma 🎰</h1>

  <div id="maquina">
    <div id="slots">
      <div id="s1">🍒</div>
      <div id="s2">🍋</div>
      <div id="s3">🍊</div>
    </div>
    <button id="boton" onclick="jugar()">🎲 GIRAR</button>
  </div>

  <div id="mensaje"></div>
  <div id="reflexion">
    <strong>¿Funciona la ludopatía?</strong><br>
    Pensaste que ganabas, pero perdiste todo.<br>
    ¿Vas a seguir, o te gusta?
  </div>

  <script>
    const simbolos = ["🍒", "🍋", "🍊", "🍉", "7️⃣", "⭐"];
    let intentos = 0;
    let terminado = false;

    function jugar() {
      if (terminado) return;

      intentos++;
      const s1 = document.getElementById("s1");
      const s2 = document.getElementById("s2");
      const s3 = document.getElementById("s3");
      const mensaje = document.getElementById("mensaje");
      const boton = document.getElementById("boton");

      // Animación rápida
      [s1, s2, s3].forEach(s => {
        s.classList.remove("rodillo");
        void s.offsetWidth; // reset
        s.classList.add("rodillo");
      });

      setTimeout(() => {
        let val1, val2, val3;
        let gano;

        if (intentos <= 3) {
          // Gana
          let simbolo = simbolos[Math.floor(Math.random() * simbolos.length)];
          val1 = val2 = val3 = simbolo;
          gano = true;
        } else if (intentos <= 5) {
          // Pierde
          val1 = simbolos[0];
          val2 = simbolos[1];
          val3 = simbolos[2];
          gano = false;
        } else {
          // Última pérdida + reflexión
          val1 = simbolos[3];
          val2 = simbolos[4];
          val3 = simbolos[5];
          gano = false;
          terminado = true;
          boton.disabled = true;
          document.getElementById("reflexion").style.display = "block";
        }

        s1.innerText = val1;
        s2.innerText = val2;
        s3.innerText = val3;
        mensaje.innerText = gano ? "¡Ganaste! 🎉" : "Perdiste 😞";
      }, 1000); // tiempo para mostrar tras animación
    }
  </script>

</body>
</html>