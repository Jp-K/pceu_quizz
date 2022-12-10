<script lang="ts">
    const items = [
        {
            question: "Which language runs in a web browser?",
            a: "Java",
            b: "C",
            c: "Python",
            d: "JavaScript",
            correct: "d",
            isAnsweredCorrectly: false,
        },
        {
            question: "What does CSS stand for?",
            a: "Central Style Sheets",
            b: "Cascading Style Sheets",
            c: "Cascading Simple Sheets",
            d: "Cars SUVs Sailboats",
            correct: "b",
            isAnsweredCorrectly: false,
        },
    ];

    let questionA:any = null;
    let questionB:any = null;
    let questionC:any = null;
    let questionD:any = null;

    function deselectAnswers() {
        questionA.checked = false;
        questionB.checked = false;
        questionC.checked = false;
        questionD.checked = false;
    }

    let currentQuestionItem = items[0];

    let questionNumber = 0;

    let correctAnswers = 0;

    let selectedAnswer = "";

    let isFinished = false;

    function submitAnswer() {
        if (!selectedAnswer) {
            return;
        }
        deselectAnswers();
        if (selectedAnswer === currentQuestionItem.correct) {
            correctAnswers++;
            items[questionNumber].isAnsweredCorrectly = true;
        }
        questionNumber++;
        if (items.length > questionNumber) {
            currentQuestionItem = items[questionNumber];
        } else {
            isFinished = true
        }
    }

</script>

<div class="body">
    <div class="quiz-container" >
        <div class="quiz-header">
            {#if !isFinished}
          <h2 id="question">{currentQuestionItem.question}</h2>
          <ul>
            <li>
              <input type="radio" name="answer" id="a" class="answer" on:click={() => selectedAnswer = "a"} bind:this={questionA}>
              <label for="a">{currentQuestionItem.a}</label>
            </li>
   
            <li>
              <input type="radio" name="answer" id="b" class="answer" on:click={() => selectedAnswer = "b"} bind:this={questionB}>
              <label for="b">{currentQuestionItem.b}</label>
            </li>
   
            <li>
              <input type="radio" name="answer" id="c" class="answer" on:click={() => selectedAnswer = "c"} bind:this={questionC}>
              <label for="c">{currentQuestionItem.c}</label>
            </li>
   
            <li>
              <input type="radio" name="answer" id="d" class="answer" on:click={() => selectedAnswer = "d"} bind:this={questionD}>
              <label for="d">{currentQuestionItem.d}</label>
            </li>
          </ul>
          {:else}
          <h2 id="question">Você acertou {correctAnswers} questões!</h2>
          {/if}
        </div>
        {#if !isFinished}
        <button on:click={submitAnswer} >Submit</button>
        {/if}
      </div>
    </div>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@200;400&display=swap');
 
 * {
    box-sizing: border-box;
 }
  
 .body {
    background-color: #b8c6db;

    background-image: linear-gradient(to right, #ff5f6d     , #ffc371);
    font-family: 'Poppins', sans-serif;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    overflow: hidden;
    margin: 0;
 }
  
 .quiz-container {
    background-color: #fff;
    border-radius: 10px;
    box-shadow: 0 0 10px 2px rgba(100, 100, 100, 0.1);
    width: 800px;
    overflow: hidden;
    box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px;
    box-shadow: rgba(0, 0, 0, 0.15) 0px 5px 15px 0px;
 }
  
 .quiz-header {
    padding: 4rem;
 }
  
 h2 {
    padding: 1rem;
    text-align: center;
    margin: 0;
 }
  
 ul {
    list-style-type: none;
    padding: 0;
 }
  
 ul li {
    font-size: 1.2rem;
    margin: 1rem 0;
 }
  
 ul li label {
    cursor: pointer; 
 }
  
 button {
    background-image: linear-gradient(to right, #ff5f6d     , #ffc371);
    color: #fff;
    border: none;
    display: block;
    width: 100%;
    cursor: pointer;
    font-size: 1.2rem;
    font-family: inherit;
    padding: 1.3rem;
    font-weight: bold;
 }
  
 button:hover {
    background-color: #732d91;
 }
  
 button:focus {
    outline: none;
    background-color: #5e3370;
 }
</style>