<script>
  import { onMount } from 'svelte';
  import { globalplugin } from './store/stores';
  import { WorkoutsArray } from "./workouts/workoutarray";
  import { ProgramArray } from "./workouts/programarray";
  import "carbon-components-svelte/css/all.css";
  import LibLoader from './components/LibLoadder.svelte';
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

  const pluginname = "Nomie 7 Mins Workout";
  const pluginemoji = "💪";
  var parent = "";
  let PlugiAapiUrl = "https://cdn.jsdelivr.net/gh/open-nomie/plugins/bin/v1/nomie-plugin.js";
  
  const plugin = new NomiePlugin({
        name: pluginname,
        emoji: pluginemoji,
        avatar: "data:image/jpeg;base64,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",
        description: "7 Minutes Workout Plugin",
        uses: ["createNote", "getTrackable","selectTrackables", "getLocation"],
        version: "1.0",
        addToCaptureMenu: true,
        addToMoreMenu: true,
        addToWidgets: false,
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
      await plugin.storage.init()
      config = await plugin.storage.getItem('configuration') || {trackers:["none"],trackeroverrule:true,logentry:"Just finished <7minswo> exercise taking <duration> minutes.",colors:{flesh:"#d5ae83",hair:"#412323",pants:"#414141",shirt:"#42cbef"}};
       if (plugin.prefs.theme == "light") {
        theme = "g10"}
      else if (plugin.prefs.theme == "dark") {
        theme = "g90"}  
      else {theme = "g10"} 
    })

   setTimeout(() => {
      inNomie = true;
      loading = false;
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

function onLoaded() {
//  setTimeout(()=>{
//  if (plugin.prefs == undefined) {
//    window.location.reload()}},2000);
 /* if (!plugin) {
  plugin = new NomiePlugin({
        name: pluginname,
        emoji: pluginemoji,
        avatar: "data:image/jpeg;base64,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",
        description: "7 Minutes Workout Plugin",
        uses: ["createNote", "getTrackable","selectTrackables", "getLocation"],
        version: "1.0",
        addToCaptureMenu: true,
        addToMoreMenu: true,
        addToWidgets: false,
      })
  } */
}

 onMount(async () => {
  loadInitParams();
 })

</script>

<LibLoader url={PlugiAapiUrl}
on:loaded="{onLoaded}" />
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
