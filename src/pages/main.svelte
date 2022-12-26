<script>
    import { createEventDispatcher } from 'svelte';
    import {
      Button,
      Content,
        Grid,
        Row,
        Column,
ContentSwitcher, 
Switch,
Tile,
    } from "carbon-components-svelte";
    import WatsonHealthStudySkip from "carbon-icons-svelte/lib/WatsonHealthStudySkip.svelte";
    export let pluginname;
    export let pluginemoji;

    let selectedDuration = 0;
    let selectedTarget = 0;

   let open=true;
   
   const dispatch = createEventDispatcher();

   function exitMain(){
        dispatch("exitinfo");
        open = false;
    }

    function startWorkout(){
    dispatch("startworkout",[selectedDuration,selectedTarget])
   } 

</script>

<Content>
    <Grid>
      <Row>
        <Column>
          <h1 style="text-align:center">{pluginemoji}</h1>
          <h2 style="text-align:center">{pluginname}</h2>
          <h5 style="text-align:center">Loaded Succesfully</h5>
          <hr>
        </Column>
      </Row>
    </Grid>
    <Tile>
      <h3>Duration:</h3>
      <ContentSwitcher size="sm" bind:selectedIndex={selectedDuration}>
        <Switch text="7 min" style="font-size:75%"/>
        <Switch text="14 min" style="font-size:75%" />
        <Switch text="21 min" style="font-size:75%" />
        <Switch text="28 min" style="font-size:75%" />
      </ContentSwitcher>
    </Tile>
    <br>
    <Tile>
      <h3>Target:</h3>
      <ContentSwitcher size="sm" bind:selectedIndex={selectedTarget}>
        <Switch text="Full Body" style="font-size:65%" />
        <Switch text="Upper Body" style="font-size:65%" />
        <Switch text="Lower Body" style="font-size:65%" />
        <Switch text="Core" style="font-size:65%" />
      </ContentSwitcher>
    </Tile>
    <br>
    <Grid>
      <Row>
        <Column style="width:20%">
        </Column>
        <Column style="width:60%">
          <Button style="width:100%" icon={WatsonHealthStudySkip} on:click={()=>{startWorkout()}}>Start</Button>
        </Column>
        <Column style="width:20%">
        </Column>
      </Row>
    </Grid>


  </Content>



  <style>
    h2 {
       margin: 0;
       padding: 0;
       font-size: 2.5em;
       font-weight: 400;
   }




 </style>

