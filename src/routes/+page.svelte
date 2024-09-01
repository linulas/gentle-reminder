<script lang="ts">
  import Button from "$lib/ui/button.svelte";
  import Timer from "$lib/ui/timer.svelte";
  import Alert from "../lib/ui/alert.svelte";

  let title = "";
  let pulse = false;
  let minutes: number;
  let seconds: number;
  let timerStarted = false;
  let intervalId: number;

  $: if (seconds > 59) {
    seconds = 59;
  }

  const decreseTimer = () => {
    console.log({ minutes, seconds, intervalId });
    seconds -= 1;

    if (minutes > 0 && seconds < 0) {
      minutes -= 1;
      seconds = 59;
    }

    if (minutes <= 0 && seconds <= 0) {
      clearInterval(intervalId);
      pulse = true;
      timerStarted = false;
    }
  };

  $: {
    if (timerStarted) {
      clearInterval(intervalId);
      intervalId = setInterval(decreseTimer, 1000);
    }
  }

  $: {
    if (pulse) {
      minutes = 0;
      seconds = 0;
    }
  }

  const startTimer = () => {
    if (!minutes) {
      minutes = 0;
    }
    if (!seconds) {
      seconds = 0;
    }

    timerStarted = true;
    console.log({ timerStarted });
  }

  const stop = () => {
    clearInterval(intervalId);
    timerStarted = false;
    minutes = 0;
    seconds = 0;
  }
</script>

<main>
  {#if !timerStarted}
    <div class="form">
      <div class="form-title">
        <label for="title"> Title </label>
        <input id="title" type="text" bind:value={title} />
      </div>

      <div>
        <!-- <label for="minutes"> Minutes </label> -->
        <input
          min={0}
          placeholder="MM"
          id="minutes"
          type="number"
          bind:value={minutes}
        />

        <!-- <label for="seconds"> Seconds </label> -->
        <input
          min={0}
          max={59}
          placeholder="SS"
          name="seconds"
          type="number"
          bind:value={seconds}
        />
        <Button onClick={startTimer} disabled={minutes <= 0 && seconds <= 0}>Start</Button>
      </div>
    </div>
  {:else}
    <Timer {minutes} {seconds} {stop} />
  {/if}

  {#if pulse}
    <Alert bind:pulse {title} />
  {/if}
</main>

<style lang="scss">
  .form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  .form-title {
    display: flex;
    flex-direction: column;
  }

  input {
    padding: 1rem;
  }

  input[type="number"] {
    width: 4rem;
  }

  :global(body) {
    margin: 0;
    background-color: $clr-background_dark;
    font-family: $font-sans-serif;
    @include text-sm;
    @media screen and (min-width: $media-sm) {
      @include text-base;
    }
  }
  :global(p, span, div, button, a, li, label) {
    @include text-sm;
    color: $clr-text-light;
    @media screen and (min-width: $media-sm) {
      @include text-base;
    }
  }

  main {
    width: calc(100% - 2rem);
    margin: auto;
    height: 100vh;
    width: 100vw;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
