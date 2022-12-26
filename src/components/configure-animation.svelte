<script lang="ts">
  
  export let flesh;
  export let hair;
  export let pants;
  export let shirt;

  let refresh = true;

  let rootElement;

	$: rootElement && rootElement.style.setProperty('--hair', `${hair}`);
  $: rootElement && rootElement.style.setProperty('--flesh', `${flesh}`);
  $: rootElement && rootElement.style.setProperty('--pants', `${pants}`);
  $: rootElement && rootElement.style.setProperty('--shirt', `${shirt}`);

  

    
</script>

<style lang="scss">
  
  * {
    .shapes > * {
    opacity: 1;
   /* --flesh: #d5ae83;
	  --hair: #412323;
    --pants: #414141;
    --shirt: #42cbef;*/
    --hair:inherit;
    --pants:inherit;
    --flesh:inherit;
    --shirt:inherit;
    width:100%;
    max-width: 400px;
    height: 400px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto;
   
  }
  }
</style>

{#if refresh}
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 538.2 564.5" height="100%" width="100%">>

  <g class="shapes" bind:this={rootElement}>
    <g id="configuration">
      <path
        d="M202 157c-2 0-2-2-1-3 4-14 8-27 14-40 3-8 9-11 16-14l31-11 9 11c2 1 1 5 4 5a70 70 0 0 0 23 0c7-1 11-6 13-13l37 17c7 3 8 10 11 15l11 31c1 4 2 8-2 10-5-3-9 0-12 3-6 4-12 6-18 8l-4-5-1 22-2 47c-1 14 1 29 2 44 1 6-1 7-6 6a20 20 0 0 0-3 0l-24 1-68-5c-3 0-5-1-7 1a1 1 0 0 1-1 0c-1-3-2-6-1-10l7-52c2-17 0-33 1-49 0-6 2-12 1-18l-5 6c-8-5-17-4-25-7Z"
        fill="var(--shirt)"
      />
      <path
        fill="var(--pants)"
        d="M225 287c2-2 4-1 7-1l68 5 24-1 1 7c-2 12-4 24-3 37a207 207 0 0 0-2 30c0 3 0 5-4 5s-5 4-8 5c-11 0-21 0-31-6a4 4 0 0 0-4 0c-11 5-23 2-35 1-7-1-9-4-9-11-1-24-5-47-4-71Z"
      />
      <path
        fill="var(--flesh)"
        d="M238 369c12 1 24 4 35-1a4 4 0 0 1 4 0c10 6 20 6 31 6l-5 29a89 89 0 0 0 1 17c3 18-3 34-7 51-4 14-8 29-8 44a14 14 0 0 1-1 6c-5-4-10-4-16 1v-17c4-13 3-27 2-40-1-12-2-23 0-34 1-7 3-14 1-22a192 192 0 0 1-3-26c-2 15-6 30-4 45 2 10 3 20 1 29-3 18-4 35 0 52 1 3 1 7-3 9-5-2-10-1-14 2 1-24-8-46-12-69-2-12-3-24-1-36 3-15 1-31-1-46ZM338 176c6-2 12-4 18-8 3-3 7-6 12-3 2 14-1 29 2 43 5 23-2 45-4 67-1 14-4 27-1 41 2 12-6 24-18 27l-9 2c-5-2-4-5-1-8s7-6 8-12c0-2 3-4 0-5-4-2-5 1-7 3a77 77 0 0 1-4 8 3 3 0 0 1-3 1 2 2 0 0 1-1-3c3-8 2-17 9-23s11-14 10-25l-1-37c-1-16 0-32-6-47-2-7-1-14-4-21ZM202 157c8 3 18 2 25 7l-1 9c-1 12-8 23-7 35a112 112 0 0 1-8 46c-4 10-6 22-2 32s6 20 6 31c0 2 1 4-2 5-2 1-3-1-4-2s-2-4-4-2c-2 1-1 3 0 5l4 8c1 1 1 4-1 5s-4 0-5-1a11 11 0 0 0-6-4l-4-6-3-8c-4-9-3-17 0-25 4-12 4-23 2-35-2-19 1-39 4-58l1-7c3-11 4-23 5-35ZM311 92c-2 7-6 12-13 13a70 70 0 0 1-23 0c-3 0-2-4-4-5l-9-11c7-5 8-15 2-23l-4-12c-1-2-2-5 2-6l3 6c0-10 0-17 3-23 2-4 4-7 8-5a34 34 0 0 0 21 0c3-1 8-1 8 3 1 6 6 11 6 18 0 1-1 3 1 4 3 0 2-3 3-4 3 3 3 12-1 16s-5 9-7 14c-2 6-2 11 4 15Z"
      />
      <path
        fill="var(--hair)"
        d="M252 520c4-3 9-4 14-2 0 4 0 7 6 4 6-5 11-5 16-1 5 8 10 16 9 25-1 13-18 19-28 12-1-1-2-2-4-1-17 8-26 1-23-18 1-7 3-14 10-19ZM315 47c-1 1 0 4-3 4-2-1-1-3-1-4 0-7-5-12-6-18 0-4-5-4-8-3a34 34 0 0 1-21 0c-4-2-6 1-8 5-3 6-3 13-3 23l-3-6c-2-10 2-21-2-32-1-3 1-5 4-6 10-6 21-9 33-6 4 1 6 4 10 6 16 10 7 24 8 37Z"
      />
    </g>
    
    </g>
  
  </svg>
  {/if}