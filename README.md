<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Quiz Corrigé : Histoire d'Auchan</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f2f2f2;
      margin: 0;
      padding: 0;
    }
    .quiz-container {
      max-width: 800px;
      margin: auto;
      background: white;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }
    h1 {
      text-align: center;
      color: #d00000;
      font-size: 1.8rem;
    }
    .question {
      margin-bottom: 20px;
    }
    .options label {
      display: block;
      margin-bottom: 5px;
      font-size: 1rem;
    }
    button {
      display: block;
      margin: 25px auto;
      padding: 12px 28px;
      background-color: #d00000;
      color: white;
      border: none;
      border-radius: 5px;
      font-size: 1rem;
      cursor: pointer;
    }
    .result, .feedback {
      text-align: center;
      font-weight: bold;
      font-size: 1.2rem;
    }
    .correct {
      color: green;
    }
    .incorrect {
      color: red;
    }

    @media (max-width: 600px) {
      .quiz-container {
        padding: 15px;
      }
      h1 {
        font-size: 1.5rem;
      }
      .options label {
        font-size: 0.95rem;
      }
      button {
        font-size: 1rem;
        padding: 10px 20px;
      }
    }
  </style>
</head>
<body>
  <div class="quiz-container">
    <h1>Quiz : L'histoire d'Auchan (Corrigé)</h1>
    <form id="quizForm">
      <!-- Questions injectées par JavaScript -->
    </form>
    <button type="button" onclick="calculateScore()">Voir le résultat</button>
    <div class="result" id="result"></div>
  </div>

  <script>
    const questions = [
      {
        q: "1. En quelle année Auchan a-t-il été fondé ?",
        options: { a: "1957", b: "1961", c: "1973", d: "1980" },
        answer: "b"
      },
      {
        q: "2. Quel est le nom du fondateur d'Auchan ?",
        options: { a: "Gérard Mulliez", b: "Louis Mulliez", c: "Pierre Mulliez", d: "Jacques Mulliez" },
        answer: "a"
      },
      {
        q: "3. Dans quelle ville Auchan a-t-il ouvert son premier magasin ?",
        options: { a: "Lille", b: "Paris", c: "Lyon", d: "Rouen" },
        answer: "a"
      },
      {
        q: "4. En quelle année Auchan a-t-il inauguré son premier hypermarché ?",
        options: { a: "1965", b: "1967", c: "1970", d: "1982" },
        answer: "b"
      },
      {
        q: "5. Combien de pays compte Auchan parmi ses implantations (environ, 2023) ?",
        options: { a: "5", b: "12", c: "20", d: "30" },
        answer: "b"
      },
      {
        q: "6. Quelle est la devise d'Auchan ?",
        options: { a: "Le pouvoir d'achat c'est maintenant", b: "On s'engage pour vous", c: "La vie, la vraie", d: "Ensemble pour demain" },
        answer: "c"
      },
      {
        q: "7. Quel est le nom du programme de fidélité d'Auchan ?",
        options: { a: "Waaoh!", b: "Maxichèque", c: "Fidéli+", d: "Club Bonus" },
        answer: "a"
      },
      {
        q: "8. En quelle année Auchan a-t-il commencé son expansion internationale ?",
        options: { a: "1981", b: "1990", c: "1989", d: "1977" },
        answer: "a"
      },
      {
        q: "9. Quelle est la couleur dominante du logo d'Auchan ?",
        options: { a: "Rouge", b: "Bleu", c: "Vert", d: "Jaune" },
        answer: "a"
      },
      {
        q: "10. Quel est le nom de la fondation créée par Auchan ?",
        options: { a: "Fondation Auchan pour la Jeunesse", b: "Fondation Famille Mulliez", c: "Fondation Solidaire", d: "Fondation Ensemble" },
        answer: "a"
      }
    ];

    const form = document.getElementById("quizForm");

    // Génère dynamiquement les questions
    questions.forEach((item, index) => {
      const qDiv = document.createElement("div");
      qDiv.classList.add("question");
      qDiv.innerHTML = `<p>${item.q}</p>`;
      Object.entries(item.options).forEach(([key, text]) => {
        qDiv.innerHTML += `
          <label>
            <input type="radio" name="q${index}" value="${key}" />
            ${text}
          </label>`;
      });
      qDiv.innerHTML += `<div class="feedback" id="feedback${index}"></div>`;
      form.appendChild(qDiv);
    });

    function calculateScore() {
      let score = 0;
      questions.forEach((item, index) => {
        const selected = document.querySelector(`input[name="q${index}"]:checked`);
        const feedback = document.getElementById(`feedback${index}`);
        if (selected) {
          if (selected.value === item.answer) {
            score++;
            feedback.innerHTML = "✔️ Bonne réponse !";
            feedback.className = "feedback correct";
          } else {
            feedback.innerHTML = `❌ Mauvaise réponse. La bonne réponse était : <strong>${item.options[item.answer]}</strong>`;
            feedback.className = "feedback incorrect";
          }
        } else {
          feedback.innerHTML = `❌ Non répondu. Réponse correcte : <strong>${item.options[item.answer]}</strong>`;
          feedback.className = "feedback incorrect";
        }
      });
      document.getElementById("result").innerText = `Score final : ${score} / ${questions.length}`;
    }
  </script>
</body>
</html>
