<script>
  import {Tile,
    } from "carbon-components-svelte";

  export let minutes = 0;
  export let seconds = 0;
  export let wodisplayname = "rest";
  export let wotime = 1;
  export let totalwotime = 1;
  export let nextwo ="";
  
  
</script>

<style>
  
  progress {
  accent-color: var(--color-primary-bright);
  width: 100%;}


</style>

<Tile>
  {#if minutes >=0}
  {#if seconds > 9}
  <p>{minutes}:{seconds}' {wodisplayname}</p>
  {:else}
  <p>{minutes}:0{seconds}' {wodisplayname}</p>
  {/if}
  {/if}
  {#if minutes <0}
  <p>0:00' {wodisplayname}</p>
  {/if}
  <progress value={wotime/totalwotime}></progress>
  <p>Next Up: {nextwo}</p>
</Tile>

   