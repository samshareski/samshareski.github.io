<script>
    import { onMount } from "svelte";

  const TIMER_MAX = 10;
  const TIMER_MIN = 0;
  let time = 0;
  let reps = 0;
  let direction = 'asc';
  /**
     * @type {number | undefined}
     */
  let interval;

  onMount(() => {
    interval = setInterval(incrementTimer, 1000);

    return () => clearInterval(interval);
  });

  let incrementTimer = () => {
    if (direction === 'asc') {
      time = time + 1;
    } else if (direction === 'dsc') {
      time = time - 1;
    }

    if (time === TIMER_MAX) {
      direction = 'dsc';
      reps = reps + 1;
    } else if (time === TIMER_MIN) {
      direction = 'asc';
      reps = reps + 1;
    }
  };

  let startTimer = () => {
    interval = setInterval(incrementTimer, 1000);
  };

  let stopTimer = () => {
    clearInterval(interval);
    interval = undefined;
  }

  let reset = () => {
    stopTimer();
    time = 0;
    reps = 0;
  }
</script>
<h3>Rep Timer</h3>
<p>{time}</p>
{#if !interval}
<button on:click={startTimer}>Start</button>
{:else}
<button on:click={stopTimer}>Stop</button>
{/if}
<button on:click={reset}>Reset</button>


