<script lang="ts">
    export let direction = "right";
    export let isPaused = false;
    export let rootElement;
    let flipsvg = false;

    if (direction == "left") {
      flipsvg = true;
    }
</script>

<style lang="scss">
  * {
    .shapes > * {
    opacity: 0;
    animation-duration: 2.5s;
    animation-iteration-count: infinite;
    animation-timing-function: steps(1);
  }
  @keyframes h-pushup-1 {
    0% {
      opacity: 1;
    }
    50%,
    100% {
      opacity: 0;
    }
  }
  #h-pushup-1 {
    animation-name: h-pushup-1;
  }
  @keyframes h-pushup-2 {
    0% {
      opacity: 0;
    }
    50%,
    100% {
      opacity: 1;
    }
  }
  #h-pushup-2 {
    animation-name: h-pushup-2;
  }

  .paused .shapes > * {
    filter: grayscale(100%);
      opacity: 0.8;
      animation-play-state: paused;
    }
  
  .flip .shapes > *{
    transform-origin: center center;
    transform: scaleX(-1); }

}
</style>

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 646 400.2" height="100%" width="100%">>
<g class:paused={isPaused} class:flip={flipsvg}>
  <g class="shapes" bind:this={rootElement}>
    <g id="h-pushup-2">
      <path
        fill="var(--shirt)"
        d="M463 256c-17-10-32-24-54-23-6-5-14-4-21-4-9-1-12-5-9-14 2-4 3-8 7-11 21-13 30-34 39-55 6-14 5-29 10-42 14 3 25 13 36 23 29 23 64 39 94 61 18 13 28 31 30 53l3 9a103 103 0 0 1-7 30c-3 0-8 1-10-1-11-9-19-4-26 5s-13 9-19 1c-2-3-3-5-7-5-10-6-20-15-33-17-8-3-14-9-23-8Z"
      />
      <path
        fill="var(--pants)"
        d="M435 107c-5 13-4 28-10 42-9 21-18 42-39 55-4-6-9-2-13-2l-3-1c-3 0-7-1-8 3a24 24 0 0 1-2 0c-26-6-44 8-64 21-7 5-15 10-25 9-9-13-11-29-13-45-1-9 0-17 9-23 4-4 4-8 0-12-1-5 0-10 5-13l60-43c32-22 68-22 95-1l8 10Z"
      />
      <path
        fill="var(--flesh)"
        d="M267 154c4 4 4 8 0 12-9 6-10 14-9 23 2 16 4 32 13 45-18 12-36 24-58 28-31 6-59 23-88 35-9 3-20 4-27 12-6-2-10 2-15 5l-19 13c-7 3-15 4-21-1-5-3-6-10-6-16 1-7 8-14 13-15 21-6 20-24 26-39 32-10 58-32 88-46 11-5 22-7 34-9 16-3 30-8 42-21 8-9 16-20 27-26ZM473 258c9-1 15 5 23 8-1 27 0 28 37 30-2-4-5-8-3-13 3 0 4 2 6 4 6 9 12 9 19 0s15-14 26-5c2 2 7 1 10 1 5 5 4 10 2 16a293 293 0 0 0-9 36c-1 4-3 11 5 11-7 5-7 12-5 18 2 7 8 1 12 2 14 3 29 2 42 10 4 3 8 7 5 10-3 5-5 14-13 11-18-6-36-4-55-4-8-1-14-4-16-14-3-18-8-36-10-55-1-11-6-13-15-11-9 1-18 3-28 1-23-5-27-7-31-30l-1-9-2-3Z"
      />
      <path
        fill="var(--hair)"
        d="M76 256c-6 15-5 33-26 39-5 1-12 8-13 15 0 6 1 13 6 16 7 5 14 4 21 1l19-13c5-3 9-7 15-5-2 9 6 8 11 9 5 2 12 2 12 9 0 8-7 9-13 9-11 2-22 5-32-3-5-2-4 0-3 3 4 12 10 21 25 21 5 0 10 3 10 9 1 6-3 8-7 11-24 13-52 8-70-13L4 329c-6-8-5-12 4-17 9-6 18-12 29-16 9-3 10-7 4-14-7-7-6-11 3-15 11-5 20-11 32-11ZM589 346c-8 0-6-7-5-11a293 293 0 0 1 9-36c2-6 3-11-2-16a103 103 0 0 0 7-30c12 9 22 20 31 32 9 14 7 29-6 40-10 9-22 14-34 21Z"
      />
    </g>
    <g id="h-pushup-1">
      <path
        fill="var(--pants)"
        d="M289 0c10 6 20 12 32 14l2 4c0 40-10 77-27 113-1 3-5 3-7 5l-7 1v-1 1c-25 0-40 19-59 32l-32-66c9-44 29-81 73-99 2-1 5-1 5-4Z"
      />
      <path
        fill="var(--shirt)"
        d="M289 136c2-2 6-2 7-5 17-36 27-73 27-113l-2-4c12-2 19 8 28 12 28 11 56 26 84 39s54 27 75 51c3 8 4 17 10 24v30c1 13-6 13-13 9-10-5-20-2-29-3-3 0-6 1-6 5 1 13-9 11-16 12-2-2-2-6-4-6-34-5-61-28-94-37-18-4-36-11-55-8-6 1-9-2-12-6Z"
      />
      <path
        fill="var(--flesh)"
        d="M454 193c7-1 17 1 16-12 0-4 3-5 6-5 9 1 19-2 29 3 7 4 15 4 13-9v-30l9 2c8 0 16 2 16 11s-9 7-15 7c-2 0-5 1-6 3 0 3 2 5 4 7 8 3 15 8 23 10s8 5 5 11l-6 9c-26-9-31-5-29 21 1 12 7 22 16 29l29 95c5 17 17 21 32 23 14 1 29 4 42 10 5 3 9 10 8 11-5 4-6 14-15 11-18-7-36-5-54-5-8-1-14-4-19-11-10-17-22-33-29-51-7-15-18-21-33-20-14 0-20-7-24-19-10-28-19-55-16-85l-2-16Zm27 31c-2 21 2 38 5 56 2 14 8 16 20 12-7-22-11-45-25-68ZM191 103l32 66c-11 2-14 12-19 19-10 14-22 24-37 33-21 12-35 31-52 48a112 112 0 0 1-18 14c-5 4-10 8-11 15-7 1-10 7-12 12-3 12-19 12-22 24l-6 2c-13 1-18-7-17-27l6-3 9-11c5-9 15-14 14-26 25-22 36-57 64-76l1-1c32-15 45-45 58-75 2-5 3-11 10-14Z"
      />
      <path
        fill="var(--hair)"
        d="M29 309c-1 20 4 28 17 27l6-2c3-12 19-12 22-24 2-5 5-11 12-12 6 12 14 23 30 23 4 0 8 1 8 6s-2 7-7 8c-17 4-34 7-47-10-2 16 5 25 18 29l15 4c5 1 11 0 11 8 0 7-5 12-10 12-10-1-19 5-28 6-19 3-33-1-46-15L6 346c-7-6-9-12 0-19 8-6 13-16 23-18ZM548 200l6-9c3-6 3-9-5-11s-15-7-23-11c-2-1-4-3-4-6 1-2 4-3 6-3 6 0 15 2 15-7 0-10-8-11-16-11l-9-2c-6-7-7-16-10-24 18 1 36-3 54 2 16 5 22 15 21 31-1 20-10 37-16 54-5 12-12 3-18 0ZM58 269c1 12-9 17-14 26l-9 11c-9-11-5-19 6-26 6-4 10-10 17-11Z"
      />
      <path fill="var(--shirt)" d="M282 137v-1 1z" />
    </g>
  </g>
</g>
    {#if isPaused}
    <svg viewBox="-6 -5 36 36" width="100%" height="100%" xmlns="http://www.w3.org/2000/svg" fill-rule="evenodd" clip-rule="evenodd"><path d="M10 24h-6v-24h6v24zm10 0h-6v-24h6v24zm-11-23h-4v22h4v-22zm10 0h-4v22h4v-22z"/></svg>
    {/if} 
  </svg>