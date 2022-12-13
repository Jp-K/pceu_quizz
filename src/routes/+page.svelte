<script lang="ts">
   import {afterUpdate} from "svelte";

   import popup from "../components/popup.svelte";

   const items = [
        //Q1
        {
            question: "Qual é o tempo mínimo necessário para uma boa escovação?",
            a: "30 segundos.",
            b: "5 minutos.",
            c: "2 minutos.",//Correta
            d: "1 minuto.",
            correct: "c",
            answer: "",
            link: "https://www.youtube.com/embed/qHI-CybmJOM",
        },
        //Q2
        {
            question: "Que tipo de escova de dente devo escolher?",
            a: "Com cerdas macias e arredondadas.",//Correta
            b: "Com cerdas macias e grandes.",
            c: "Com cerdas duras e pequenas.",
            d: "Com cerdas duras e grandes.",
            correct: "a",
            answer: "",
            link: "https://www.youtube.com/embed/qHI-CybmJOM",
        },
        //Q3
        {
            question: "Qual a maneira correta de escovar os dentes?",
            a: "Suavemente e devagar.",//Correta
            b: "Com força e devagar.",
            c: "Suavemente e rápido.",
            d: "Com força e rápido.",
            correct: "a",
            answer: "",
            link: "https://www.youtube.com/embed/qHI-CybmJOM",
        },
        //Q4
        {
            question: "Qual a frequência ideal para escovar os dentes?",
            a: "Logo após as refeições.",
            b: "Ao acordar e antes de dormir.",
            c: "3 Vezes ao dia.",
            d: "30 minutos após as refeições.",//Correta
            correct: "d",
            answer: "",
            link: "https://www.youtube.com/embed/qHI-CybmJOM",
        },
        //Q5
        {
            question: "Quanta pasta de dente uma criança deve colocar na escova?",
            a: "Deve cobrir todas as cerdas.",
            b: "Apenas um pouco, aproximadamente um grão de ervilha.",
            c: "Bem pouco, aproximadamente um grão de arroz.",//Correta
            d: "Não é necessário pasta de dente.",
            correct: "c",
            answer: "",
            link: "https://www.youtube.com/embed/qHI-CybmJOM",
        },
        //Q6
        {
            question: "Qual é a maneira correta de passar o fio dental?",
            a: "Entrar com o fio entre os dentes e puxar.",
            b: "Entrar para além da margem da gengiva de cada dente, passar de um lado para o outro abraçando dente.",//Correta
            c: "Entrar com o fio entre os dentes, passar de um lado para o outro.",
            d: "Entrar para além da margem da gengiva de cada dente e pressionar bastante, passar de um lado para o outro abraçando dente. ",
            correct: "b",
            answer: "",
            link: "https://www.youtube.com/embed/KRnoAF7Y0nk",
        },
        //Q7
        {
            question: "Qual a frequência ideal para passar o fio dental?",
            a: "Antes de dormir.",
            b: "Sempre antes de cada escovação.",//Correta
            c: "Sempre depois de escovar os dentes.",
            d: "Apenas quando há algo incomodando.",
            correct: "b",
            answer: "",
            link: "https://www.youtube.com/embed/KRnoAF7Y0nk",
        },
        //Q8
        {
            question: "Qual destes alimentos ajuda na proteção contra a cárie?",
            a: "Refrigerante.",
            b: "Bolacha.",
            c: "Pão.",
            d: "Queijo.",//Correta
            correct: "d",
            answer: "",
            link: "https://www.youtube.com/embed/2KhX5JkHglY"
        },
        //Q9
        {
            question: "Com qual frequência a criança deve ir ao dentista?",
            a: "Uma vez a cada 6 meses.",//Correta
            b: "Uma vez por ano.",
            c: "Sempre que sentir um desconforto.",
            d: "Uma vez a cada 3 meses.",
            correct: "a",
            answer: "",
            link: "https://www.youtube.com/embed/poskbiF78BA",
        },
        //Q10
        {
            question: "A partir de que idade devemos ir ao dentista?",
            a: "Assim que nascer o primeiro dente.",
            b: "Entre 8 meses e 2 anos.",
            c: "Antes dos 8 meses.",//Correta
            d: "Assim que nascer o primeiro dente permanente.",
            correct: "c",
            answer: "",
            link: "https://www.youtube.com/embed/Cdo__xPd5-s"
        },
    ];

    let questionA:HTMLInputElement;
    let questionB:HTMLInputElement;
    let questionC:HTMLInputElement;
    let questionD:HTMLInputElement;

    function deselectAnswers() {
        
        questionA.checked = false;
        questionB.checked = false;
        questionC.checked = false;
        questionD.checked = false;
        selectedAnswer = "";
    }

    let currentQuestionItem = items[0];

    let questionNumber = 0;

    let correctAnswers = 0;

    let selectedAnswer = "";

    let isFinished = false;

    let currentResultItem = 0;

    let popupElement:any;

    let resultElements: HTMLElement[] = [];

    let randomItem:any = items[0];

   function retornarValorAleatorio(lista) {
       if (Array.isArray(lista) && lista.length > 0) {
           const indiceAleatorio = Math.floor(Math.random() * lista.length);

           return lista[indiceAleatorio];
       } else {
           return undefined;
       }
   }

    function submitAnswer() {
        if (!selectedAnswer) {
            return;
        }

        correctAnswers = selectedAnswer === currentQuestionItem.correct ? correctAnswers+1 : correctAnswers;
        items[questionNumber].answer = selectedAnswer;

        questionNumber++;
        if (items.length > questionNumber) {
            currentQuestionItem = items[questionNumber];
        } else {
            const lista = [];
            items.forEach((item) => {
                if(item.correct !== item.answer) {
                    lista.push(item)
                }
            });
            randomItem = retornarValorAleatorio(lista);
            popupElement.openPopup();

            isFinished = true
        }

        deselectAnswers();
    }

    function verifyResultIndex(index: number): string {
        if (index === currentResultItem) {
            return 'left: 0';
        }

        if (index < currentResultItem) {
            return 'left: -800px'
        }

        return '';
    }

    function swipeResult(modifier: number) {
        currentResultItem = currentResultItem+modifier;

        for (let i = 0; i < resultElements.length; i++) {
            const eleStyle = resultElements[i].style;

            if (i === currentResultItem) {
                eleStyle.left = "0px";
            } else if (i < currentResultItem) {
                eleStyle.left = "-800px";
            } else {
                eleStyle.left = "800px";
            }
        }
    }

    afterUpdate(() => {
        const currentElement = resultElements[currentResultItem];
        const currentAnswer = items[currentResultItem];

        if (!currentElement) {
            return;
        }

        const responses = currentElement.querySelectorAll('li');


        for (let liElement of responses) {
            const letter = liElement.innerText.split(")")[0].toLowerCase();
            console.log(letter, currentAnswer.correct, currentAnswer.answer)

            if (letter === currentAnswer.correct) {
                liElement.style.backgroundColor = "rgba(0,255,43,0.7)";
            }

            if (letter === currentAnswer.answer && letter !== currentAnswer.correct) {
                liElement.style.backgroundColor = "rgba(255,0,0,0.7)";
            }
        }
    })

</script>

<div class="body">
    <svelte:component this={popup} bind:this={popupElement} question={randomItem.question} VideoLink={randomItem.link}/>
    <div class="quiz-container" >
        <div class="quiz-header">
            {#if !isFinished}
          <h2>{currentQuestionItem.question}</h2>
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
                <h2>Você acertou {correctAnswers} questões!</h2>
                <div class="results-container">
                    {#each items as question, index}
                        <div class="result-item" bind:this={resultElements[index]} style={verifyResultIndex(index)}>
                            <h2>{question.question}</h2>
                            <ul>
                                <li>
                                    <strong>A) </strong> <span>{question.a}</span>
                                </li>

                                <li>
                                    <strong>B) </strong><span>{question.b}</span>
                                </li>

                                <li>
                                    <strong>C) </strong><span>{question.c}</span>
                                </li>

                                <li>
                                    <strong>D) </strong><span>{question.d}</span>
                                </li>
                            </ul>
                        </div>

                    {/each}
                    <div style="gap: 15px; display: flex; max-width: 700px; position: relative; top: 400px">
                        {#if currentResultItem !== 0}
                        <button on:click={() => swipeResult(-1)}>voltar</button>
                            {/if}
                        {#if currentResultItem !== items.length-1}
                        <button on:click={() => swipeResult(1)}>próximo</button>
                            {/if}
                    </div>

                </div>

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

 .results-container {
     position: relative;
     width: 800px;
     height: 500px;
 }

 .result-item {
     position: absolute;
    width: 800px;
     height: 500px;
     left: 800px;
     top:0;
     transition: ease;
     transition-duration: 1s;
     max-width: 700px;
 }

 .result-item > h2 {
     max-width: 700px;
 }

 .result-item li {
     padding: 5px;
     border-radius: 25px;
 }

</style>