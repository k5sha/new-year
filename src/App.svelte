<script>
  import christmas_tree from '/christmas_tree.png';
  import Timer from './lib/Timer.svelte';
  import {onMount} from "svelte";
  import {writable} from "svelte/store";

  const windowWidth = writable(window.innerWidth || 12);

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
  <div class="garland">
    {#each Array(Math.max(Math.floor($windowWidth / 25), 12)) as _, i}
      <span class="light" style="--index: {i};"></span>
    {/each}
  </div>
  <div class="tree-container">
    <a href="https://svelte.dev" target="_blank" rel="noreferrer">
      <img src={christmas_tree} class="logo" alt="Christmas tree" />
    </a>
  </div>
  <h1>Happy new year {new Date().getFullYear() + 1}</h1>

  <div class="card">
    <Timer />
  </div>
</main>

<style>
  .tree-container {
    position: relative;
    display: inline-block;
  }

  .logo {
    height: 12em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
    animation: logo 5s infinite;
  }

  @keyframes logo {
    0%, 100% {
      filter: drop-shadow(0 0 2em rgba(100, 255, 154, 0.67));
    }
    50% {
      filter: drop-shadow(0 0 2em rgba(100, 255, 154, 0.3));
    }
  }


  .garland {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    flex-wrap: nowrap;
    justify-content: center;
    pointer-events: none;
  }

  .light {
    width: 10px;
    height: 10px;
    background-color: #dd4141;
    border-radius: 50%;
    margin: 2px;
    animation: blink 2s infinite;
  }

  .light:nth-child(2n) {
    background-color: #4fd74f;
  }

  .light:nth-child(3n) {
    background-color: #5252bd;
  }

  .light:nth-child(4n) {
    background-color: #cfcf57;
  }

  .light:nth-child(5n) {
    background-color: #d7d4d4;
  }

  .light:nth-child(odd) {
    animation-delay: calc(var(--index) * 0.1s);
  }

  @keyframes blink {
    0%, 100% {
      opacity: 1;
    }
    50% {
      opacity: 0.4;
    }
  }
</style>
