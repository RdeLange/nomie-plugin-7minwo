<script>
  import { onMount } from 'svelte';
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
    import { tweened } from 'svelte/motion';
    import Controller from '../components/program-controller.svelte';
    import Workoutprogress from '../components/workout-progress.svelte';
    import WorkoutAnimation from "../components/workout-animation.svelte";


    export let pluginname;
    export let pluginemoji;
    export let plugin;
    export let duration = 6.5;
    export let target = "full";
    export let program;
    //export let equipment = "nothing";
    export let workouts;
    export let flesh;
    export let hair;
    export let pants;
    export let shirt;
    export let parent;
    export let settingsconfig;

   let open=true;
   
   const dispatch = createEventDispatcher();

   let totaltime = duration * 60;
    let timer = tweened(totaltime)
    let isPaused = false;
    let totalwotime = 10;
    let cumwotime =0;
    let wotimer = tweened(totalwotime);
    let wotime = 1;
    let wominutes = 0
    let woseconds = 10;
    let wostart;
    let woname;
    let wodisplayname;
    let wodirection;
    let activeIndexrefreshed = true;
    let nextwo = "";

    let numberofWO = 0;
    let currentWO = 0;
    let woInterval;

    
    $: minutes = Math.floor($timer / 60);
    $: seconds = Math.floor($timer - minutes * 60) ;
    $: wominutes = Math.floor($wotimer / 60);
    $: woseconds = Math.floor($wotimer - wominutes * 60) ;
    $: wotime = Math.floor($wotimer);

    $: if($wotimer <=0){
        currentWO = currentWO+1;
        if (currentWO < program.routine.length && $timer > 0) {
            nextWO();
        }
        else {programFinished()}

    }
    
    
   
    
    function startProgram(){

        numberofWO = program.routine.length;
        currentWO = 0;
        
        setInterval(() => {if(!isPaused) {
        if ($timer > 0) $timer--;}
        }, 1000);

        nextWO();
        
    }

    function nextWO() {
        if(woInterval){
        clearInterval(woInterval);}
        let wonext = [{"displayname":"Rest"}];
        let wo = workouts.filter((temp) => {
            return temp.id == program.routine[currentWO];
        });
        
        if (currentWO==program.routine.length-1){
            wonext[0].displayname = "Rest";}
        else {
            wonext = workouts.filter((temp) => {
            return temp.id == program.routine[currentWO+1];})}
        
            //validate if workout is defined, otherwise assign wo with id 40 = boxing
        if (wo.length == 0){
            wo = workouts.filter((temp) => {
            return temp.id == 40;
            });}
        if (wonext.length == 0){
            wonext = workouts.filter((temp) => {
            return temp.id == 40;
            });}
        //end validate

        //set workout variables
        wodisplayname = wo[0].displayname;
        woname = wo[0].woname;
        wodirection = wo[0].wodirection;
        totalwotime = wo[0].duration-0.7;
        nextwo = wonext[0].displayname
        //end set workout variable

        //change animation
        activeIndexrefreshed = false;
        setTimeout(()=>{activeIndexrefreshed = true}, 3);
        //end change animation

        //start wotimer
        wotimer = tweened(totalwotime);
        woInterval = setInterval(() => {if(!isPaused) {
        if ($wotimer > 0) $wotimer--;}
        }, 1000);
        //end start wotimer

    }
    
   function pause(){
    isPaused = true;
   }

   async function endProgram() {
    let exercisetime = (duration*60)-$timer;
    dispatch("finishedworkout",{"finaltime":exercisetime,"target":target,"early":true});
     }
	

    async function programFinished(){
       isPaused = true;
       let exercisetime = (duration*60)
       dispatch("finishedworkout",{"finaltime":exercisetime,"target":target,"early":false});

  }

  

  
    onMount(() => {
    startProgram();
    });

</script>

<Content>
    <Grid>
      <Row>
        <Column>
          <h1 style="text-align:center">{pluginemoji}</h1>
          <h2 style="text-align:center">{pluginname}</h2>
          <h5 style="text-align:center">Workout</h5>
          <hr>
        </Column>
      </Row>
    </Grid>
  </Content>
  <Controller bind:minutes bind:seconds bind:target bind:isPaused on:end={async()=>{endProgram()}}></Controller>
  {#if activeIndexrefreshed}
  <WorkoutAnimation bind:flesh bind:hair bind:pants bind:shirt bind:wo_animation={woname} bind:isPaused={isPaused} direction={wodirection}></WorkoutAnimation>
  {/if}
  <Workoutprogress bind:nextwo={nextwo} bind:minutes={wominutes} bind:seconds={woseconds} bind:wotime={wotime} bind:totalwotime={totalwotime} bind:wodisplayname={wodisplayname}></Workoutprogress>

  <style>
    h2 {
       margin: 0;
       padding: 0;
       font-size: 2.5em;
       font-weight: 400;
   }




 </style>

