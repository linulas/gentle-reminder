<script lang="ts">
  export let kind = "primary";
  export let onClick;
  export let disabled = false;
</script>

<button on:click={onClick} class={kind} {disabled}>
  <slot />
</button>

<style lang="scss">
  .primary {
    background: linear-gradient(127deg, $pink-600, $cyan-600);

    &:not(&:disabled) {
      &:hover {
        background: linear-gradient(127deg, $pink-700, $cyan-700);
      }
    }
  }
  button {
    border: none;
    border-radius: 0.5rem;
    padding: 0.5rem;

    &:disabled {
      background: $neutral-500;
    }
  }
</style>
