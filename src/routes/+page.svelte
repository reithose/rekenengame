<script>
  import "../style.css";
  import Game from "../components/Game.svelte";
  import FancyTitleWithColors from "../components/FancyTitleWithColors.svelte";
  import Footer from "../components/Footer.svelte";

  let resetSom;
</script>

<main class="container mx-auto grid pt-9 place-items-center">
  <div class="bg-white max-w-4xl drop-shadow-2xl rounded-lg p-9">
    <div>
      <FancyTitleWithColors title="Oefenen voor het tafeldiploma!" />
    </div>
    <div class="mt-4 grid grid-cols-1 place-content-center">
      <div class="md:w-1/3 mx-auto">Geef het antwoord en druk op enter</div>
    </div>
    <div class="mt-4 grid grid-cols-1 place-content-center">
      <div class="md:w-1/2 mx-auto"><Game /></div>
    </div>
    <div class="mt-4 grid grid-cols-1 place-content-center">
      <div class="md:w-1/2 mx-auto"><Footer /></div>
    </div>
  </div>
</main>
