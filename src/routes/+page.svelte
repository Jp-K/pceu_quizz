<script lang="ts">
   const items = [
        //Q1
        {
            question: "Qual é o tempo mínimo necessário para uma boa escovação",
            a: "30 segundos.",
            b: "5 minutos.",
            c: "2 minutos.",//Correta
            d: "1 minuto.",
            correct: "c",
            isAnsweredCorrectly: false,
        },
        //Q2
        {
            question: "Que tipo de escova de dente devo escolher?",
            a: "Com cerdas macias e arredondadas.",//Correta
            b: "Com cerdas macias e grande.",
            c: "Com cerdas duras e pequena.",
            d: "Com cerdas duras e grande.",
            correct: "a",
            isAnsweredCorrectly: false,
        },
        //Q3
        {
            question: "Qual a maneira correta de escovar os dentes?",
            a: "Devagar e suave.",//Correta
            b: "Forte e devagar.",
            c: "Forte e suave.",
            d: "Devagar e forte.",
            correct: "a",
            isAnsweredCorrectly: false,
        },
        //Q4
        {
            question: "Qual a frequência ideal para escovar os dentes?",
            a: "Logo após as refeições.",
            b: "Ao acordar e antes de dormir.",
            c: "3 Vezes ao dia.",
            d: "30 minutos após as refeições.",//Correta
            correct: "d",
            isAnsweredCorrectly: false,
        },
        //Q5
        {
            question: "Quanta pasta de dente uma criança deve colocar na escova?",
            a: "Deve cobrir todas as cerdas.",
            b: "Apenas um pouco, aproximadamente um grão de ervilha.",
            c: "Bem pouco, aproximadamente um grão de arroz.",//Correta
            d: "Não é necessário pasta de dente.",
            correct: "c",
            isAnsweredCorrectly: false,
        },
        //Q6
        {
            question: "Qual é a maneira correta de passar o fio dental?",
            a: "Entrar com o fio entre os dentes e puxar.",
            b: "Entrar para além da margem da gengiva de cada dente, passar de um lado para o outro abraçando dente.",//Correta
            c: "Entrar com o fio entre os dentes, passar de um lado para o outro.",
            d: "Entrar para além da margem da gengiva de cada dente e pressionar bastante, passar de um lado para o outro abraçando dente. ",
            correct: "b",
            isAnsweredCorrectly: false,
        },
        //Q7
        {
            question: "Qual a frequência correta de passar o fio dental?",
            a: "Antes de dormir.",
            b: "Sempre antes de cada escovação.",//Correta
            c: "Sempre depois de escovar os dentes.",
            d: "Apenas quando há algo incomodando.",
            correct: "b",
            isAnsweredCorrectly: false,
        },
        //Q8
        {
            question: "Qual alimento ajudar a na proteção contra a cárie?",
            a: "Refrigerante.",
            b: "Bolacha.",
            c: "Pão.",
            d: "Queijo.",//Correta
            correct: "d",
            isAnsweredCorrectly: false,
        },
        //Q9
        {
            question: "Com qual frequência a criança deve ir ao dentista?",
            a: "Uma vez a cada 6 meses.",//Correta
            b: "Uma vez por ano.",
            c: "Sempre que sentir um desconforto.",
            d: "Uma vez a cada 3 meses.",
            correct: "a",
            isAnsweredCorrectly: false,
        },
        //Q10
        {
            question: "A partir de que idade devemos ir ao dentista?",
            a: "Assim que nascer o primeiro dente.",
            b: "Antes dos 2 anos.",
            c: "Antes dos 8 meses.",//Correta
            d: "Assim que nascer o primeiro dente permanente.",
            correct: "c",
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