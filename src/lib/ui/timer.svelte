<script lang="ts">
  import { fade } from "svelte/transition";
  import StopIcon from "./stop_icon.svelte";

  export let seconds: number;
  export let minutes: number;
  export let stop: () => void;

  const hoverColor = "#1f2937";
  const idleColor = "#111827";

  let color = idleColor;

  $: minutesDisplay = minutes < 10 ? `0${minutes}` : minutes.toString();
  $: secondsDisplay = seconds < 10 ? `0${seconds}` : seconds.toString();

  const setColor = (value: string) => {
    color = value;
  };
</script>

<!-- svelte-ignore a11y-no-static-element-interactions -->
<div
  class="wrapper"
  in:fade={{ duration: 200 }}
  on:mouseenter={() => setColor(hoverColor)}
  on:mouseleave={() => setColor(idleColor)}
>
  <div class="timer">
    <span>{minutesDisplay}:{secondsDisplay}</span>
    <button on:click={stop}>
      <StopIcon fill={color} />
    </button>
  </div>
</div>

<style lang="scss">
  .wrapper {
    width: 100vw;
    height: 100vh;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #111827;
    display: flex;
    justify-content: center;
    align-items: center;

    &:hover {
      span {
        color: #1f2937;
      }
    }

    span {
      color: #111827;
      font-size: 4rem;
    }
  }

  .timer {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2rem;
  }

  button {
    background-color: unset;
    border: none;
  }
</style>
