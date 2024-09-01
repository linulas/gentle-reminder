<script lang="ts">
export let fill = "url(#stop-icon-gradient)"; 
</script>
<svg
  style="width:0;height:0;position:absolute;"
  aria-hidden="true"
  focusable="false"
>
  <linearGradient id="stop-icon-gradient" x2="1" y2="1">
    <stop offset="25%" stop-color="#db2777" />
    <stop offset="75%" stop-color="#22d3ee" />
    <stop offset="100%" stop-color="#0891b2" />
  </linearGradient>
</svg>

<svg
  fill={fill}
  enable-background="new 0 0 512 512"
  height="512px"
  id="Layer_1"
  version="1.1"
  viewBox="0 0 512 512"
  width="512px"
  xml:space="preserve"
  xmlns="http://www.w3.org/2000/svg"
  xmlns:xlink="http://www.w3.org/1999/xlink"
  ><path
    d="M256,512C114.625,512,0,397.375,0,256C0,114.609,114.625,0,256,0s256,114.609,256,256C512,397.375,397.375,512,256,512z   M256,64C149.969,64,64,149.969,64,256s85.969,192,192,192c106.03,0,192-85.969,192-192S362.031,64,256,64z M192,192h128v128H192  V192z"
  /></svg
>

<style lang="scss">
  svg {
    width: 4rem;
    height: 4rem;
    transition: fill .2s ease;
    transition: scale .2s ease;

    &:hover {
      scale: 110%;
    }
  }
</style>
