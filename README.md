<!DOCTYPE html>
<html lang="it">
<head>
  <meta charset="UTF-8">
  <title>Test Divino</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background-color: #ffe6ea;
      text-align: center;
      padding: 50px;
    }
    h1 {
      color: #d10000;
    }
    input, button {
      padding: 10px;
      font-size: 18px;
      border-radius: 8px;
      border: none;
      margin-top: 20px;
    }
    #giudizio {
      margin-top: 30px;
      font-size: 20px;
      font-weight: bold;
    }
    #originalita {
      margin-top: 15px;
      width: 300px;
      height: 20px;
      background-color: #ddd;
      border-radius: 10px;
      margin-left: auto;
      margin-right: auto;
    }
    #barra {
      height: 100%;
      background-color: #ff0000;
      width: 0%;
      border-radius: 10px;
      transition: width 1s;
    }
    #immagine {
      margin-top: 20px;
      max-width: 300px;
      display: none;
    }
    #condividiBtn {
      display: none;
      margin-top: 20px;
      background-color: #333;
      color: white;
    }
  </style>
</head>
<body>
  <h1>Test Divino 2.0</h1>
  <p>Scrivi una bestemmia e vediamo cosa dice il cielo...</p>
  <input type="text" id="bestemmia" placeholder="Scrivi qui...">
  <br>
  <button onclick="lanciaGiudizio()">Lancia il Giudizio</button>

  <div id="giudizio"></div>
  <div id="originalita"><div id="barra"></div></div>
  <img id="immagine" src="">
  <br>
  <button id="condividiBtn" onclick="condividi()">Condividi con gli amici</button>

  <script>
    const frasi = {
      dio: [
        "Dio ha sentito... ed è andato in ferie.",
        "Hai fatto tremare il Vaticano.",
        "Pure l'Anticristo si è segnato.",
        "Gesù ha disinstallato la vita.",
        "Un fulmine sta cercando casa tua."
      ],
      madonna: [
        "La madonna ha cambiato pianeta.",
        "Anche i santi hanno messo il silenzioso.",
        "Maria ha chiesto un avvocato.",
        "I cherubini si sono nascosti.",
        "Ci sono più porci che santi qui dentro."
      ],
      gesù: [
        "Gesù ha tolto l'amicizia su Facebook.",
        "Hai sbloccato la bestemmia leggendaria.",
        "Gesù si è dato alla boxe.",
        "Crociate 2.0 in arrivo.",
        "Anche Ponzio Pilato si è commosso."
      ],
      santi: [
        "I santi stanno preparando una denuncia.",
        "Hai fatto bestemmiare anche un prete.",
        "I santi sono in sciopero.",
        "Paradiso chiuso per manutenzione.",
        "Satana ti ha offerto un contratto."
      ],
      generico: [
        "Pure Google si è bloccato.",
        "Anche l'inferno ti ha segnalato.",
        "È partita una chiamata celeste.",
        "Il Papa ha ricevuto una notifica.",
        "L'acqua santa ha cambiato sapore."
      ]
    };

    const immagini = {
      dio: "https://i.imgur.com/EdybDnT.jpg",
      madonna: "https://i.imgur.com/fZYtZ7B.jpg",
      gesù: "https://i.imgur.com/DQJFNBg.jpg",
      santi: "https://i.imgur.com/o8kQvE2.jpg",
      generico: "https://i.imgur.com/KVcpjRE.jpg"
    };

    function lanciaGiudizio() {
      const testo = document.getElementById('bestemmia').value.toLowerCase();
      let tipo = 'generico';

      if (testo.includes("dio")) tipo = 'dio';
      else if (testo.includes("madonna")) tipo = 'madonna';
      else if (testo.includes("gesù") || testo.includes("gesu")) tipo = 'gesù';
      else if (testo.includes("santo") || testo.includes("santi")) tipo = 'santi';

      const frase = frasi[tipo][Math.floor(Math.random() * frasi[tipo].length)];
      const percento = Math.floor(Math.random() * 81) + 20;

      document.getElementById("giudizio").innerText = frase;
      document.getElementById("barra").style.width = percento + "%";
      document.getElementById("immagine").src = immagini[tipo];
      document.getElementById("immagine").style.display = "block";
      document.getElementById("condividiBtn").style.display = "inline-block";

      // Salva per condivisione
      document.getElementById("condividiBtn").setAttribute("data-frase", testo);
      document.getElementById("condividiBtn").setAttribute("data-risposta", frase);
      document.getElementById("condividiBtn").setAttribute("data-originalita", percento);
    }

    function condividi() {
      const frase = document.getElementById("condividiBtn").getAttribute("data-frase");
      const risposta = document.getElementById("condividiBtn").getAttribute("data-risposta");
      const originalita = document.getElementById("condividiBtn").getAttribute("data-originalita");

      const text = `[Test Divino 2.0]\nFrase: ${frase}\nRisposta: ${risposta}\nOriginalità: ${originalita}%`;
      navigator.clipboard.writeText(text).then(() => {
        alert("Copiato! Incola e invia dove vuoi.");
      });
    }
  </script>
</body>
</html>
