<script>
    import {afterUpdate} from "svelte";
    let popup;

    export function openPopup() {
        popup.classList.add("open-popup")
    }

    export function closePopup() {
        popup.classList.remove("open-popup")
    }
</script>


<div class="popup" bind:this={popup}>
    <h2>Este é o conteúdo do meu popup.</h2>
    <button type="button" on:click={closePopup}>Ok</button>
</div>

<style>
    * {
        box-sizing: border-box;
        font-family: 'Poppins', sans-serif;
    }
    :global(.popup){
        z-index: 10;
        width: 400px;
        background-color: #fff;
        border-radius: 6px;
        position: absolute;
        left: 50%;
        top: 0;
        transform: translate(-50%, -50%) scale(0.1);
        text-align: center;
        padding: 0 30px 30px;
        color: #333;
        visibility: hidden;
        transition: transform 0.4s, top 0.4s;
    }

    :global(.open-popup){
        visibility: visible;
        top: 50%;
        transform: translate(-50%, -50%) scale(1);
    }

    :global(.popup) h2{
        font-size: 38px;
        font-weight: 500;
        margin: 30px 0 10px;
    }

    :global(.popup) button{
        width: 100%;
        margin-top: 50px;
        padding: 10px 0;
        background: #6fd649;
        color: #fff;
        border: 0;
        outline: none;
        font-size: 18px;
        border-radius: 4px;
        cursor: pointer;
        box-shadow: 0 5px 5px rgba(0, 0, 0, 0.2);
    }
</style>