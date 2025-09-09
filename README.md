index.html
==========
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="style.css">
    
</head>
<body>
    <h1>Rock Paper Scissors</h1>

    <div class="choices">
        <div class="choice" id="rock"><img src="rock.png"></div>
        <div class="choice" id="Paper"><img src="paper.png"></div> 
        <div class="choice" id="Scissor"><img src="scissors.png"></div>
    </div>

<div class="score-board">
    <div class="score">
        <p id="user-score">0</p>
        <p>you</p>
    </div>
     <div class="score">
        <p id="comp-score">0</p>
        <p>comp</p>
    </div>
</div>
    <div class="msg-container">
        <p id="msg">play your move</p>
    </div>

style.css
=========
*{
    margin: 0;
    padding: 0;
    text-align: center;
}

h1{
    background-color: #081b31;
    color: #fff;
    height: 5rem;
    line-height: 5rem;
}
.choice{
    height: 140px;
    width: 140px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;

}
img{
    height: 135px;
    width: 135px;
    border-radius: 50%;
    object-fit: cover;

}
.choices{
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 5rem;
    gap: 3rem;
}
.choice:hover{
    
    cursor: pointer;
    /* opacity: 0.5; */
    background-color: #081b31;
}
.score{
    
    align-items: center;
    justify-content: center;
  }
  .score-board{
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2rem;
    margin-top: 3rem;
    gap: 5rem;
  }

  #user-score,#comp-score{
      font-size: 4rem;
  }
  .msg-container{
    margin-top: 5rem;
  }

  #msg{
    background-color: #081b31;
    color: #fff;
    font-size: 2rem;
    margin-top: 5rem;
    display: inline;
    padding: 1rem;
    border-radius: 1rem;
  }

  script.js
  =========
  let userScore = 0;
let compScore = 0;

const choices = document.querySelectorAll(".choice");
const msg = document.querySelector("#msg");
const userScoreElem = document.querySelector("#user-score");
const compScoreElem = document.querySelector("#comp-score");

const getCompChoice = () => {
    const options = ["rock", "paper", "scissor"];
    const randomIdx = Math.floor(Math.random() * 3);
    console.log(randomIdx);
    return options[randomIdx];
};

const drawGame = () => {
    msg.innerText = "It's a draw!";
    msg.style.backgroundColor = "#ffa500";
};

const showWinner = (userWin, userChoice, compChoice) => {
    if (userWin) {
        userScore++;
        userScoreElem.innerText = userScore;
        msg.innerText = `You win! ${userChoice} beats ${compChoice}`;
        msg.style.backgroundColor = "green";
    } else {
        compScore++;
        compScoreElem.innerText = compScore;
        msg.innerText = `You lose! ${compChoice} beats ${userChoice}`;
        msg.style.backgroundColor = "red";
    }
};

const playGame = (userChoice) => {
    const compChoice = getCompChoice();

    if (userChoice === compChoice) {
        drawGame();
    } else {
        let userWin = false;
        if (
            (userChoice === "rock" && compChoice === "scissor") ||
            (userChoice === "scissor" && compChoice === "paper") ||
            (userChoice === "paper" && compChoice === "rock")
        ) {
            userWin = true;
        }
        showWinner(userWin, userChoice, compChoice);
    }
};

choices.forEach((choice) => {
    choice.addEventListener("click", () => {
        const userChoice = choice.getAttribute("id").toLowerCase();
        playGame(userChoice);
    });
});




<script src="script.js"></script>
</body>
</html>
