<script lang="ts">
  import StopIcon from "./stop_icon.svelte";

  export let pulse = false;
  export let title: string | undefined;
</script>

<div class:pulse>
  {#if pulse}
    <div class="title">
      {#if title}
        <p>
          {title}
        </p>
      {/if}
      <button on:click={() => (pulse = false)}>
        <StopIcon />
      </button>
    </div>
  {/if}
</div>

<style lang="scss">
  div {
    z-index: 100;
    display: flex;
    align-items: center;
    justify-content: center;
    position: absolute;
    top: 50%;
    left: 50%;
    width: 100vw;
    height: 100vh;
    transform: translate(-50%, -50%);
  }

  .title {
    p {
      font-size: 2rem;
      margin: 1rem;
    }
    display: flex;
    flex-direction: column;
  }

  .pulse {
    animation: pulse 0.75s infinite alternate;
  }

  button {
    z-index: 1000;
    background-color: unset;
    border: none;
  }

  @keyframes pulse {
    0% {
      background-color: $gray-900;
    }
    50% {
      background-color: $gray-900;
    }
    100% {
      background-color: $gray-700;
    }
    50% {
      background-color: $gray-700;
    }
  }
</style>
