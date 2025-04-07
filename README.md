<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Pierre Papier Ciseaux</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background: linear-gradient(135deg, #667eea, #764ba2);
      color: white;
      text-align: center;
      padding: 2rem;
    }
    .choices button {
      font-size: 1.2rem;
      margin: 1rem;
      padding: 1rem 2rem;
      border: none;
      border-radius: 10px;
      background-color: #4fd1c5;
      color: white;
      cursor: pointer;
      transition: background 0.3s;
    }
    .choices button:hover {
      background-color: #38b2ac;
    }
    .result {
      margin-top: 2rem;
      font-size: 1.5rem;
    }
  </style>
</head>
<body>
  <h1>Pierre, Papier, Ciseaux</h1>
  <div class="choices">
    <button onclick="jouer('pierre')">Pierre</button>
    <button onclick="jouer('papier')">Papier</button>
    <button onclick="jouer('ciseaux')">Ciseaux</button>
  </div>
  <div class="result" id="result"></div>

  <script>
    let dernierCoupJoueur = null;

    function battre(coup) {
      const regles = {
        pierre: "papier",
        papier: "ciseaux",
        ciseaux: "pierre"
      };
      return regles[coup];
    }

    function jouer(joueur) {
      let bot;
      if (dernierCoupJoueur) {
        bot = battre(dernierCoupJoueur);
      } else {
        const choix = ["pierre", "papier", "ciseaux"];
        bot = choix[Math.floor(Math.random() * 3)];
      }

      let resultat = "";
      if (joueur === bot) {
        resultat = `Égalité ! Vous avez tous les deux joué ${joueur}.`;
      } else if (bat(joueur, bot)) {
        resultat = `Bravo ! Tu as gagné. (${joueur} bat ${bot})`;
      } else {
        resultat = `Le bot gagne... (${bot} bat ${joueur})`;
      }

      document.getElementById("result").textContent = resultat;
      dernierCoupJoueur = joueur;
    }

    function bat(a, b) {
      return (a === "pierre" && b === "ciseaux") ||
             (a === "papier" && b === "pierre") ||
             (a === "ciseaux" && b === "papier");
    }
  </script>
</body>
</html>
