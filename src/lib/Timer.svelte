<script>
  import {onDestroy, onMount} from "svelte";

  const newYear = new Date(`Jan 1 ${new Date().getFullYear() + 1} 00:00:00`);

  function getTimeToNewYear() {
    const diff = newYear.getTime() - new Date().getTime() ;
    const seconds = Math.floor((diff / 1000) % 60);
    const minutes = Math.floor((diff / 1000 / 60) % 60);
    const hours = Math.floor((diff / 1000 / 60 / 60) % 24);
    const days = Math.floor(diff / 1000 / 60 / 60 / 24);

    return {days, hours, minutes, seconds};
  }

  let time = getTimeToNewYear();
  let timer_interval;

  onMount(() => {
    timer_interval = setInterval(() => {
      time = getTimeToNewYear();
    }, 1000);
  });

  onDestroy(() => clearInterval(timer_interval));
</script>

<time>
  {time.days} days, {time.hours} hours, {time.minutes} minutes, {time.seconds} seconds
</time>
