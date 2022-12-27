<script>
  import { onMount } from 'svelte';
  import { globalplugin } from './store/stores';
  import { WorkoutsArray } from "./workouts/workoutarray";
  import { ProgramArray } from "./workouts/programarray";
  import "carbon-components-svelte/css/all.css";
  import {
    Header,
    HeaderUtilities,
    HeaderGlobalAction,
    SkipToContent,
    Content,
    Grid,
    Row,
    Column,
    Theme,
    Button,
  } from "carbon-components-svelte";
  import Main from "./pages/main.svelte";
  import Info from "./pages/info.svelte";
  import Settings from "./pages/settings.svelte";
  import Workout from "./pages/workout.svelte";
  import SettingsAdjust from "carbon-icons-svelte/lib/SettingsAdjust.svelte";
  import Sun from "carbon-icons-svelte/lib/Sun.svelte";
  import Information from "carbon-icons-svelte/lib/Information.svelte";

  const pluginname = "7 Mins Workout";
  const pluginemoji = "💪";
  var parent = "";
  
  const plugin = new NomiePlugin({
        name: pluginname,
        emoji: pluginemoji,
        description: "7 Minutes Workout Plugin",
        uses: ["createNote", "getTrackable","selectTrackables", "getLocation"],
        version: "1.0",
        addToCaptureMenu: true,
        addToMoreMenu: true,
        addToWidgets: true,
      }); 
  let inNomie = false;
  let isSideNavOpen = false;
  let theme = "g10";
  let mode = "hidden";
  let loading = true;
  let view = "main";

  //plugin params
  let programduration = 0;
  let programtarget = 0;
  var config;
  let workouts;
  let woprogram;
  let woequipment;
  let woduration;
  let wotarget;

  // Load init params
  function loadInitParams() {
    parent = getParentUrl();
    globalplugin.set(plugin);
    plugin.onUIOpened(async () => {
      mode = 'modal';
    });

    plugin.onWidget(() => {
      if (plugin.prefs.theme == "light") {
        theme = "white"}
      else if (plugin.prefs.theme == "dark") {
        theme = "g100"}  
      else {theme = "g10"} 
      mode = "widget";
    });

    plugin.onRegistered(async () => {
      inNomie = true;
      loading = false;
      await plugin.storage.init()
      config = await plugin.storage.getItem('configuration') || {trackers:["none"],trackeroverrule:true,logentry:"Just finished <7minswo> exercise taking <duration> minutes.",colors:{flesh:"#d5ae83",hair:"#412323",pants:"#414141",shirt:"#42cbef"}};
       if (plugin.prefs.theme == "light") {
        theme = "g10"}
      else if (plugin.prefs.theme == "dark") {
        theme = "g90"}  
      else {theme = "g10"} 
    })

    setTimeout(() => {
      if (loading) {
        inNomie = false;
      }
    }, 700);
  }

  // change theme
  function toggleTheme(){
    console.log(theme);
    if (theme == "white"){
      theme = "g10"}
    else if (theme == "g10"){
      theme = "g80"}
    else if (theme == "g80"){
      theme = "g90"}
    else if (theme == "g90"){
      theme = "g100"}
    else {
      theme = "white"}
 }

  // Get parent
  function getParentUrl() {
    var isInIframe = (parent !== window),
        parentUrl = null;

    var parentfound = null;
    
    if (isInIframe) {
        parentUrl = document.referrer;
    }

    if (parentUrl.includes("nomie")) {
      parentfound = "Nomie"
    }
    else {parentfound = "Smarter4Ever"}

    return parentfound;
}

//view main page
function showMain(){
  view = "main"
  window.scrollTo(0,0);
 }
 
 //view info page
 function showInformation(){
  view = "info"
  window.scrollTo(0,0);
 }

 //view settings page
 function showSettings(){
  view = "settings"
  window.scrollTo(0,0);
 }

 function saveSettings(payload){
  config = payload.detail;
  plugin.storage.setItem('configuration', config);
  showMain();
 }

 function exitSettings(payload){
  config = payload.detail;
    showMain();
 }

 function exitExercise() {
  showMain();
 }

 const getRandomInt = (min, max) => {
  const bottom = Math.ceil(min);
  const top = Math.floor(max);
  return Math.floor(Math.random() * (top - bottom) + bottom);
  // Maximum is exclusive and minimum is inclusive
};

 function startWorkout(payload){
  if (payload.detail[0] == 0){
    programduration = 6.5
  }
  if (payload.detail[0] == 1){
    programduration = 13.16
  }
  if (payload.detail[0] == 2){
    programduration = 19.83
  }
  if (payload.detail[0] == 3){
    programduration = 26.5
  }

  if (payload.detail[1] == 0){
    programtarget = "full"
  }
  if (payload.detail[1] == 1){
    programtarget = "upper"
  }
  if (payload.detail[1] == 2){
    programtarget = "lower"
  }
  if (payload.detail[1] == 3){
    programtarget = "core"
  }

  //programtarget = payload.detail[1]
  calculateProgram(programtarget,programduration)
 
 }

 function calculateProgram(primaryTarget,duration){
    const matchingPrograms = ProgramArray.filter(
      (item) => item.target === primaryTarget
    );
    const min = 0;
    const max = matchingPrograms.length;
    var program1;
    var program2;
    var program3;
    var program4;
    var merged;
    var FinalProgram;
    if (duration == 6.5 ){
      
        FinalProgram=matchingPrograms[getRandomInt(min, max)];}
      else if (duration == 13.16){
        program1 = matchingPrograms[getRandomInt(min, max)];
        program2 = matchingPrograms[getRandomInt(min, max)];
        merged = {
          id: 999,
          target: primaryTarget,
          routine: [...program1.routine, 0, ...program2.routine],
        };
        FinalProgram = merged;}
      else if (duration == 19.83){
        program1 = matchingPrograms[getRandomInt(min, max)];
        program2 = matchingPrograms[getRandomInt(min, max)];
        program3 = matchingPrograms[getRandomInt(min, max)];
        merged = {
          id: 999,
          target: primaryTarget,
          routine: [
            ...program1.routine,
            0,
            ...program2.routine,
            0,
            ...program3.routine,
          ],
        };
        FinalProgram = merged;}
      else if (duration == 26.5){
        program1 = matchingPrograms[getRandomInt(min, max)];
        program2 = matchingPrograms[getRandomInt(min, max)];
        program3 = matchingPrograms[getRandomInt(min, max)];
        program4 = matchingPrograms[getRandomInt(min, max)];
        merged = {
          id: 999,
          target: primaryTarget,
          routine: [
            ...program1.routine,
            0,
            ...program2.routine,
            0,
            ...program3.routine,
            0,
            ...program4.routine,
          ],
        };
        FinalProgram = merged;
    }
    
    const equipment =
    FinalProgram.routine.indexOf(49) !== -1 || FinalProgram.routine.indexOf(50) !== -1
        ? 'Chair'
        : 'Nothing';
    
    woduration = duration;
    wotarget = primaryTarget;
    woprogram = FinalProgram;
    woequipment = equipment;
    workouts = WorkoutsArray;    
    view = "workout";}

    async function finishedWorkout(payload){
      if(payload.detail.early){
        var res1 = {};
      res1 = await plugin.confirm('Really stop Session?', 'The current session will be ended now');
      if(res1.value) {
        console.log("They DID CONFIRM it");
        await delay(200);
      } else {
        console.log("They DID NOT CONFIRM it");
        return;
      }
    }
  

        var finaltime = payload.detail.finaltime/60;
        var target = payload.detail.target;
        console.log(finaltime);
        if (config.trackers[0] != "none") {
        var res = null;
        res = await plugin.confirm('Save Results?', 'Concratulations, you finished your workout. Would you like to log your results?');

         if (res.value) {
          await delay(200);
           
            if(config.trackeroverrule){
  
    var res3 = null;
    res3 = await plugin.confirm('Log session to '+parent, 'This will log your session in '+parent+ ' as you configured via settings');
   // res.value = confirm("Log session");
      if (res3.value) {
        let trackinglog ="";
          if (config.trackers[0] != "None") {
            let timertrack = "#"+config.trackers[0]+"("+(finaltime*60)+")";
            trackinglog = timertrack+"\n";
          }
          let logentry = config.logentry;
        logentry = logentry.replace("<duration>", finaltime.toString());
        logentry = logentry.replace("<7minwo>", target);
        const note = "7 Minutes Workout 💪:\n"+logentry+"\n\n"+trackinglog;
        plugin.createNote(note);
        
        }
      }
    
    }
    else {
        console.log("User does not want to save")
        

    }} 
    else {
        console.log("Nothing will be saved as settings are not configured")
        plugin.alert("Congratulation!", "Congratulations, you finalised a workout. You do not have any settings on how to log this in "+parent+" so nothing will be logged");
       
    }
    showMain();
    
     }    

     function delay(time) {
  return new Promise(resolve => setTimeout(resolve, time));
}

 onMount(async () => {
  loadInitParams();
 })

</script>


{#if mode == "modal"  || mode =="widget"}
<Theme bind:theme />
{#if inNomie}
{#if mode == "modal"}
<Header company={parent} platformName={pluginname} on:click={showMain}>
  <svelte:fragment slot="skip-to-content">
    <SkipToContent />
  </svelte:fragment>
  <HeaderUtilities>
    <HeaderGlobalAction aria-label="Settings" icon={SettingsAdjust} on:click={showSettings}/>
    <HeaderGlobalAction aria-label="Theme" icon={Sun} on:click={toggleTheme}/>
    <HeaderGlobalAction aria-label="Theme" icon={Information} on:click={showInformation}/>
  </HeaderUtilities>
</Header>

{#if view == "main"}
<Main pluginname={pluginname} pluginemoji={pluginemoji} on:startworkout={(e)=>{startWorkout(e)}}/>
{:else if view == "info"}
<Info parent={parent} pluginname={pluginname} pluginemoji={pluginemoji} on:exitinfo={showMain}/>
{:else if view == "settings"}
<Settings pluginname={pluginname} pluginemoji={pluginemoji} plugin={plugin} theme={theme} settingsconfig={config} on:exitsettings={(e)=>{exitSettings(e)}} on:savesettings={(e)=>{saveSettings(e)}}/>
{:else if view == "workout"}
<Workout pluginname={pluginname} pluginemoji={pluginemoji} plugin={plugin} parent={parent} settingsconfig={config} bind:flesh={config.colors.flesh} bind:hair={config.colors.hair} bind:pants={config.colors.pants} bind:shirt={config.colors.shirt} duration={woduration} target={wotarget} workouts={workouts} program={woprogram} equipment={woequipment} on:finishedworkout={(e)=>{finishedWorkout(e)}}/>
{/if}
{:else if mode == "widget"}
<p>Widget Placeholder</p>
{/if}
{/if}

{:else if !inNomie}
        <h1 style="text-align:center">{pluginemoji}</h1>
        <h2 style="text-align:center">{pluginname}</h2>
        <h5 style="text-align:center">This is a plugin for {parent}</h5>
        <hr>
{/if}
{#if loading}
<div class="startup">
<p>Loading....</p>
</div>
{/if}
