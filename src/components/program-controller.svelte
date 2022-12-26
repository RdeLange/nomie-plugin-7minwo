<script>
  import { createEventDispatcher, onMount } from "svelte";
  import { globalplugin } from '../store/stores';
  import {
    ContentSwitcher, 
    Switch,
    Tile,
    } from "carbon-components-svelte";

  export let minutes;
  export let seconds;
  export let target;
  export let isPaused = false;
  let plugin;
  const unsubscribe = globalplugin.subscribe((value) => plugin = value)
  let pausebutton = `Pause`;
  let wotarget = "Full Body";

  const dispatch = createEventDispatcher();

  if(target == "full"){
    wotarget = "Full Body";
  }
  else if(target == "upper"){
    wotarget = "Upper Body";
  }
  else if(target == "lower"){
    wotarget = "Lower Body";
  }
  else { wotarget = "Core";}

  function setPause(){
    if (!isPaused) {
      isPaused = true;
      pausebutton = `Resume`;
    } 
    else {
      isPaused = false;
      pausebutton = `Pause`;
    }
}

  async function letEnd(){
    dispatch("end");
  
  }

  
</script>

<style>
  
</style>

{#if minutes >=0}
  {#if seconds > 9}
  <h3 style="text-align:center">{wotarget} Workout {minutes}:{seconds}'</h3>
  {:else}
  <h3 style="text-align:center">{wotarget} Workout {minutes}:0{seconds}'</h3>
  {/if}
  {/if}
  {#if minutes <0}
  <h3 style="text-align:center">{wotarget} Workout 0:00'</h3>
  {/if}

<Tile>
  
  <ContentSwitcher>

    <Switch text={pausebutton} style="font-size:100%" enabled={isPaused} on:click={setPause}/>
    {#if isPaused}
    <Switch text="End" style="font-size:100%" enabled={!isPaused} on:click={letEnd}/>
    {/if}
  </ContentSwitcher>

</Tile>
   