<script>

import { sanat } from './data'

export let naytaTakaa = false;

let flashcardIndex = 0;
$: kysymys = sanat[flashcardIndex].kuva;
$: vastaus = sanat[flashcardIndex].sana;

function edellinenKortti() {
  flashcardIndex--;
}

function seuraavaKortti() {
  flashcardIndex++;
}

</script>

<main>

  <div class="flip-box">
    <div class="flip-box-inner" class:kaanto={naytaTakaa}>
      <div class="flip-box-front">
        <img src="{kysymys}" alt="{vastaus}">
      </div>
      <div class="flip-box-back">
        <h2>{vastaus}</h2>
      </div>
    </div>
  </div>

<div class="napit">
  <div class="edellinen">
    {#if flashcardIndex !== 0}
    <button on:click={edellinenKortti}>Edellinen</button>    
    {/if}
  </div>
  
  <div class="korttiVastaus">
  <button on:click={() => (naytaTakaa = !naytaTakaa)}>Näytä Vastaus</button>
  </div>

  <div class="seuraava">
    {#if flashcardIndex !== 7}
    <button on:click={seuraavaKortti}>Seuraava</button>    
    {/if}
  </div>
</div>

</main>

<style>

  img {
    max-height: 100%;
   }

.flip-box {
  background-color: transparent;
  width: 300px;
  height: 200px;
  border: 1px solid #f1f1f1;
  perspective: 1000px;
}

.flip-box-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

.kaanto {
  transform: rotateY(180deg);
}

.flip-box-front, .flip-box-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
}

.flip-box-front {
  background-color: orangered;
  color: black;
}

.flip-box-back {
  background-color: orangered;
  color: white;
  transform: rotateY(180deg);
}

</style>