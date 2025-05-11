const questions = [
  {
    question: "What cheese is known for its holes?",
    choices: ["Cheddar", "Brie", "Swiss", "Parmesan"],
    answer: "Swiss"
  },
  {
    question: "Which cheese is typically used on pizza?",
    choices: ["Feta", "Mozzarella", "Blue Cheese", "Ricotta"],
    answer: "Mozzarella"
  },
  {
    question: "Which cheese is soft and often comes in a white rind?",
    choices: ["Cheddar", "Brie", "Gouda", "Camembert"],
    answer: "Brie"
  }
];

let currentQuestion = 0;
let score = 0;

const questionEl = document.getElementById("question");
const choicesEl = document.getElementById("choices");
const nextBtn = document.getElementById("nextBtn");
const resultEl = document.getElementById("result");

function showQuestion() {
  let q = questions[currentQuestion];
  questionEl.textContent = q.question;
  choicesEl.innerHTML = "";

  q.choices.forEach(choice => {
    const btn = document.createElement("button");
    btn.textContent = choice;
    btn.onclick = () => selectAnswer(choice);
    choicesEl.appendChild(btn);
  });
}

function selectAnswer(choice) {
  const correct = questions[currentQuestion].answer;
  if (choice === correct) score++;
  currentQuestion++;

  if (currentQuestion < questions.length) {
    showQuestion();
  } else {
    showResult();
  }
}

function showResult() {
  document.getElementById("quiz-container").style.display = "none";
  resultEl.style.display = "block";
  resultEl.textContent = `You scored ${score} out of ${questions.length}!`;
}

nextBtn.style.display = "none";
showQuestion();
