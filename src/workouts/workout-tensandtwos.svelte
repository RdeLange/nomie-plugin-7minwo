<script lang="ts">
     export let isPaused = false;
     export let rootElement;
</script>

<style lang="scss">
  * {
    .shapes > * {
    opacity: 1;
    animation: flip 5s linear infinite;
    animation-timing-function: steps(1);
  
  @keyframes flip {
    0%,
    24.99999999% {
      transform-origin: center center;
      transform: scaleX(1);
    }
    25%,
    49.99999999% {
      transform-origin: center center;
      transform: scaleX(-1);
    }
    50%,
    74.99999999% {
      transform-origin: center center;
      transform: scaleX(1);
    }
    75%,
    100% {
      transform-origin: center center;
      transform: scaleX(-1);
    }
  }
    
  }

  .paused .shapes > * {
    filter: grayscale(100%);
      opacity: 0.8;
      animation-play-state: paused;
  }
  
  }
</style>

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 511 262.4" height="100%" width="100%">
  <g class:paused={isPaused}>
    <g class="shapes" bind:this={rootElement}>
      <g id="flip">
        <path
          d="m281 240-14 11c-5 3-9 6-15 7l-18 4h-9c-13-2-23-11-33-19-4-3-6-8-8-12a76 76 0 0 0-22-31 29 29 0 0 1-7-8c-1-2-2-4-1-6a10 10 0 0 1 4 3c5 5 12 7 19 7 4-1 8-2 10-6 1-2 2-3 0-5l-3-4v-2l11-4c8-3 17-5 24-10 4-2 7-5 7-11l-2-6c4-1 6 2 9 4l25 20a4 4 0 0 0 2 1l16 5a13 13 0 0 1 5 2c4 3 7 7 8 12 3 6 6 12 4 19a78 78 0 0 1-7 19l-5 10Z"
          fill="var(--pants)"
        />
        <path
          fill="var(--hair)"
          d="M29 78 5 71a3 3 0 0 1-2-3 17 17 0 0 1 0-5c2-7 1-13-1-20l-2-9a19 19 0 0 1 2-12C7 13 13 5 22 0h1c5 2 6 7 8 12l4-5 4-2c3-3 6-1 6 3a116 116 0 0 0 4 22c3 9 6 17 12 24a2 2 0 0 1 1 1 6 6 0 0 1-3 0c-7-1-12 3-14 9l2 10c2 7 1 6-5 5l-13-1Z"
        />
        <path
          fill="var(--flesh)"
          d="m29 78 14 1c5 1 6 2 4-5l-2-10c1-6 7-10 14-9a6 6 0 0 0 3 0s0 1 0 0l36 20 42 20 13 6a34 34 0 0 0 17 2c4 0 7 2 10 4 13 10 24 22 36 33a21 21 0 0 0 2 2l6 6 2 6c0 6-3 9-7 11-7 5-16 7-24 10l-11 4c-1 0-2 1-1 2l4 4c2 2 1 3 0 5-2 4-6 5-10 6-8 0-14-2-19-7a10 10 0 0 0-4-3l-5-9-2-1a101 101 0 0 0-25 2 5 5 0 0 0-4 2 13 13 0 0 1-6 5l-8 4a8 8 0 0 1-4 2c-3 0-4-1-3-3a6 6 0 0 1 3-3l5-3c-3-1-7 2-9 4l-3 4h-2l-1-2 1-4-3 1h-2a2 2 0 0 1 0-2c2-3 3-7 7-9a13 13 0 0 0 4-2 24 24 0 0 1 14-4 37 37 0 0 0 15-3 32 32 0 0 1 12-2c3 0 3 0 2-3a8 8 0 0 0-7-5 103 103 0 0 1-21-5 32 32 0 0 1-16-13c-6-8-13-16-21-23L50 93c-6-6-12-10-19-13l-2-2Z"
        />
        <path
          d="m224 148-6-6 23-12a13 13 0 0 1 7-2h15c3 0 5 0 7-2h39c9 0 17 4 26 6l1 1c1 3 3 3 5 3a2 2 0 0 1 3 2 2 2 0 0 0 2 1c4 0 7 2 10 3l15 5v2l-10 17a4 4 0 0 0 2 6c-2 3-3 3-7 2l-12-6a7 7 0 0 0-5 0l-8 2-2 2c-2 6-2 12-5 18l-6 17-7 11-2 2c-5 6-8 14-15 18a65 65 0 0 1-10 2 5 5 0 0 1-3 0l5-10a78 78 0 0 0 7-19c2-7-1-13-4-19-2-5-4-9-8-12a13 13 0 0 0-5-2l-17-5a4 4 0 0 1-1-1l-25-20c-3-2-6-5-9-4Z"
          fill="var(--shirt)"
        />
        <path
          fill="var(--flesh)"
          d="M363 172a4 4 0 0 1-2-6l10-17v-2l31 4 18 5c9 4 18 6 27 8l16 3 21 3c6 0 11 2 17 3l6 2a2 2 0 0 1 1 3c-1 1 0 2 1 2a7 7 0 0 1 1 1l1 2-3 1-6-2 3 6v2h-2a17 17 0 0 1-8-4 33 33 0 0 0-8-5 6 6 0 0 0-3 0 3 3 0 0 0-2 5 14 14 0 0 0 4 2c2 0 5 4 5 6s-1 3-4 2l-6-4-13-5a14 14 0 0 1-6-5c-3-4-6-5-11-4l-16 1c-15 2-29-2-43-5a63 63 0 0 0-10-2h-19ZM309 126h-39a10 10 0 0 1 2-3 9 9 0 0 0 2-6c-1-5 0-10 2-15l9-10c4-2 8-5 13-2 8 4 13 11 11 21l-1 4c1 2 3 0 4 1 1 4-1 7-3 10Z"
        />
        <path
          fill="var(--hair)"
          d="M312 116c-1-1-3 1-4-1l1-4c2-10-3-17-11-21-5-3-9 0-13 2l-9 10a40 40 0 0 1 4-10c5-10 18-9 24-3a19 19 0 0 1 6 9c2 5 4 9 3 14a11 11 0 0 1-1 4ZM62 55c0 1 0 0 0 0Z"
        />
      </g>
</g>
</g>
{#if isPaused}
<svg viewBox="-6 -5 36 36" width="100%" height="100%" xmlns="http://www.w3.org/2000/svg" fill-rule="evenodd" clip-rule="evenodd"><path d="M10 24h-6v-24h6v24zm10 0h-6v-24h6v24zm-11-23h-4v22h4v-22zm10 0h-4v22h4v-22z"/></svg>
{/if}
</svg>