<script>
  import christmas_tree from '/christmas_tree.png';
  import Timer from './lib/Timer.svelte';
  import { onMount } from "svelte";
  import { writable } from "svelte/store";

  const windowWidth = writable(window.innerWidth || 12);
  const jokes = [
    "Why do you need a jeweler on New Year’s Eve? To ring in the new year!",
    "What do cows say on January 1st? Happy Moo Year!",
    "Why should you put your calendar in the freezer? To start the year off in a cool way!",
    "What’s a New Year’s resolution? Something that goes in one year and out the other!"
  ];

  let randomJoke = "";

  function getNewJoke() {
    randomJoke = jokes[Math.floor(Math.random() * jokes.length)];
  }

  function updateWindowWidth() {
    windowWidth.set(window.innerWidth);
  }

  onMount(() => {
    window.addEventListener('resize', updateWindowWidth);
    return () => {
      window.removeEventListener('resize', updateWindowWidth);
    };
  });
</script>

<main>
  <!-- Garland at the top -->
  <div class="garland">
    {#each Array(Math.max(Math.floor($windowWidth / 25), 12)) as _, i}
      <span class="light" style="--index: {i};"></span>
    {/each}
  </div>

  <!-- Christmas Tree -->
  <div class="tree-container">
    <img src={christmas_tree} class="logo" alt="Christmas tree"/>
  </div>

  <!-- New Year Greeting -->
  <h1>Happy New Year {new Date().getFullYear() + 1}</h1>

  <!-- Timer and Joke -->
  <div class="card">
    <Timer/>
    <button on:click={getNewJoke}>Tell Me a Joke!</button>
    {#if randomJoke}
      <p class="joke">{randomJoke}</p>
    {/if}
  </div>

  <!-- Footer -->
  <footer>
    <p>Created with ❤️ by <strong>k5sha</strong></p>
  </footer>
</main>
