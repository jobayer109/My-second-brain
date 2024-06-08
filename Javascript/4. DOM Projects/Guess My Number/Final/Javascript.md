```javascript
"use strict";

const secretNum = Math.floor(Math.random() * 20) + 1;
document.querySelector(".number").textContent = secretNum;

let score = 20;
const checkBtn = document.querySelector(".check");
checkBtn.addEventListener("click", function () {
  const guess = Number(document.querySelector(".guess").value);

  // When guessing start
  if (!guess) {
    document.querySelector(".message").textContent = `⛔  No number inserted `;

  // Winning logic
  } else if (guess === secretNum) {
    document.querySelector(".message").textContent = `✌️  Correct number ! `;
    document.querySelector("body").style.backgroundColor = "#60b347";
    document.querySelector(".number").style.borderRadius = "50%";
    document.querySelector(".number").style.backgroundColor = "black";
    document.querySelector(".number").style.color = "white";
 

   // Too high guessing
  } else if (guess > secretNum) {
    if (score > 1) {
      document.querySelector(".message").textContent = `📈  Too High `;
      score--;
      document.querySelector(".score").textContent = score;

   // Game over
    } else {
      document.querySelector(".message").textContent = `💔 Game over `;
      document.querySelector(".score").textContent = 0;
    }
 

    // Too low guessing
  } else if (guess < secretNum) {
    document.querySelector(".message").textContent = `📉  Too Low `;
    score--;
    document.querySelector(".score").textContent = score;
  }
});

  
// Again Button handle

```


