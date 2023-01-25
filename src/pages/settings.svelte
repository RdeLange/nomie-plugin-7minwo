<script>
    import { createEventDispatcher , onMount } from 'svelte';
    import {
      Button,
      Content,
        Grid,
        Row,
        Column,
        Tile,
        Checkbox,
        TextInput,
    } from "carbon-components-svelte";
    import ConfigureAnimation from "../components/configure-animation.svelte";
    import ColorPicker from '../components/color-picker.svelte';
    import AccessibilityColor from "carbon-icons-svelte/lib/AccessibilityColor.svelte";
    import List from "carbon-icons-svelte/lib/TextAlignJustify.svelte";
    import CheckboxIndeterminate from "carbon-icons-svelte/lib/CheckboxIndeterminate.svelte";
   
    export let pluginname;
    export let pluginemoji;
    export let plugin;
    export let settingsconfig;
    export let theme;
   
    let flesh = '#d5ae83';
	  let hair = '#412323';
    let pants = '#414141';
    let shirt= '#42cbef';
    const lastflesh = settingsconfig.colors.flesh;
    const lasthair = settingsconfig.colors.hair;
    const lastpants = settingsconfig.colors.pants;
    const lastshirt = settingsconfig.colors.shirt;
    const lasttrackers = settingsconfig.trackers[0];
    const lastlogentry = settingsconfig.lastlogentry;
    const lasttrackeroverrule = settingsconfig.trackeroverrule;
    
    var refreshed = true;
    let trackersDisplay =["∅ None","∅ None"];

   let open=true;
   
   const dispatch = createEventDispatcher();

   // Set background
	let themecolor = "#E9E9E9";
	let themefont = "#161616"
	if(theme=="g10"){
		themecolor = "grey";
		themefont = "#161616"
	}
	else {themecolor = "lightgrey";
	themefont = "#F4F4F4"}

   $: if(settingsconfig){
      initConfig();
    }

    

   function exitSettings(){
    settingsconfig.colors.flesh = lastflesh;
      settingsconfig.colors.hair = lasthair;
      settingsconfig.colors.pants = lastpants;
      settingsconfig.colors.shirt = lastshirt;
      settingsconfig.trackers[0] = lasttrackers;
      settingsconfig.logentry = lastlogentry;
      settingsconfig.trackeroverrule = lasttrackeroverrule;
       
       dispatch("exitsettings",settingsconfig)
      open = false;
    }

    function saveSettings(){
        dispatch("savesettings",settingsconfig);
        open = false;
    } 

    function setDefaultColor(){
      settingsconfig.colors.flesh = '#d5ae83';
      settingsconfig.colors.hair = '#412323';
      settingsconfig.colors.pants = '#414141';
      settingsconfig.colors.shirt = '#42cbef';
  }

  const addTracker = async (id) => {
      const justOneTrackable = await plugin.selectTrackables('tracker',false);
      if(justOneTrackable) {
        settingsconfig.trackers[id]=justOneTrackable[0].tracker.tag;
        trackersDisplay[id]=justOneTrackable[0].tracker.emoji+" "+justOneTrackable[0].tracker.label;
      }
      
    }

    const removeTracker = async (id) => {
      settingsconfig.trackers[id] = "none";
      trackersDisplay[id] = "∅ None";
}

async function initConfig(){
     // trackeroverrule = settingsconfig.trackeroverrule;
     // trackers = settingsconfig.trackers;
     // logentry = settingsconfig.logentry;
      //trackers
      let trackable1;
      if (settingsconfig.trackers[0] != "none") {
      trackable1 = await plugin.getTrackable('#'+settingsconfig.trackers[0]);}
      else { trackable1 = {trackable:{tracker:{label:"None",emoji:"∅"}}}};
      
      trackersDisplay =[trackable1.trackable.tracker.emoji+" "+trackable1.trackable.tracker.label];
      }

      onMount (() =>{
      initConfig();
     // initTemplates();

    })

</script>

<Content>
    <Grid>
      <Row>
        <Column>
          <h1 style="text-align:center">{pluginemoji}</h1>
          <h2 style="text-align:center">{pluginname}</h2>
          <h5 style="text-align:center">Plugin Settings</h5>
          <hr>
        </Column>
      </Row>
    </Grid>
    <Tile>
      {#if refreshed}
      <div class="human">
      <ConfigureAnimation bind:flesh={settingsconfig.colors.flesh} bind:hair={settingsconfig.colors.hair} bind:pants={settingsconfig.colors.pants} bind:shirt={settingsconfig.colors.shirt}></ConfigureAnimation>
    </div>
    <span on:click={()=>{setDefaultColor()}}><AccessibilityColor size={32} style="cursor: pointer;margin-top:-32px;"/></span>
      <div class="row">
        <div class="column1">
          <p>Flesh</p>
        </div>
        <div class="column2">
        <ColorPicker bind:value={settingsconfig.colors.flesh}/>
        </div>
        </div>
        <div class="row">
          <div class="column1">
            <p>Hair</p>
          </div>
          <div class="column2">
          <ColorPicker bind:value={settingsconfig.colors.hair}/>
          </div>
          </div>
          <div class="row">
            <div class="column1">
              <p>Pants</p>
            </div>
            <div class="column2">
            <ColorPicker bind:value={settingsconfig.colors.pants}/>
            </div>
            </div>
            <div class="row">
              <div class="column1">
                <p>Shirt</p>
              </div>
              <div class="column2">
              <ColorPicker bind:value={settingsconfig.colors.shirt}/>
              </div>
              </div>
              {/if}
    </Tile>
    <br>
    <Tile>
      <h4>Log Settings:</h4>
        <Checkbox disabled labelText="Overrule individual Tracker Alignment" value={settingsconfig.trackeroverrule} />
        
       <h3>Fast Duration:</h3>
        <tr>
          <td style="vertical-align:middle; text-align:center;width:20px"><span on:click={()=>{removeTracker(0)}}><CheckboxIndeterminate size={32} style="color:{themecolor};cursor: pointer;display:table-cell;vertical-align:middle;margin-top:0px"></CheckboxIndeterminate></span></td>
          <td style="vertical-align:middle; text-align:center;width:20px"><span on:click={()=>{addTracker(0)}}><List size={32} style="color:{themecolor};cursor: pointer;display:table-cell;vertical-align:middle;margin-top:0px;"></List></span></td>
          <td style="vertical-align:middle ;text-align:left;width:250px"><p style="display:inline;font-weight:300;text-align:left;vertical-align:middle;">{trackersDisplay[0]}</p></td>
       </tr>
       <h3>Additional Log Entry Input:</h3>
       <TextInput bind:value={settingsconfig.logentry} placeholder="Enter additional Log input..."  helperText="You can include a reference to the related 7 Minutes Workout. For instance: I just did a <7minswo> workout for <duration> hours."/>
      </Tile>
    <Row>
      <Column>
          <br>
           <span><Button kind="secondary" on:click={exitSettings} style="float: left;">Exit</Button></span>
           <br>
      </Column>
    <Column>
        <br>
         <span><Button on:click={saveSettings} style="float: right;">Save</Button></span>
         <br>
    </Column>
</Row>
  </Content>



  <style>
    h2 {
       margin: 0;
       padding: 0;
   font-size: 2.5em;
   font-weight: 400;
 }

 
 h3 {
   font-size:1.2em;
   font-weight: 300;
 }


   .column1 {
  float: left;
  width: 20%;
  height: max-content;
}
.column2 {
  float: left;
  width: 80%;
  height: max-content;
}

/* Clear floats after the columns */
.row:after {
  content: "";
  display: table;
  clear: both;
}

.human {
  height: 250px;
}

 </style>

