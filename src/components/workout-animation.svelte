<script lang="ts">
    import { onMount } from "svelte";
   
    export let wo_animation = "pushups";
    export let isPaused = false;
    export let direction = "right";
	export let flesh;
    export let hair;
    export let pants;
    export let shirt;

    let Workout;
	
	let rootElement;

	$: rootElement && rootElement.style.setProperty('--hair', `${hair}`);
    $: rootElement && rootElement.style.setProperty('--flesh', `${flesh}`);
    $: rootElement && rootElement.style.setProperty('--pants', `${pants}`);
    $: rootElement && rootElement.style.setProperty('--shirt', `${shirt}`);

    const sleep = ms => new Promise(f => setTimeout(f, ms));

    async function loadAnimation(){
		if (wo_animation == "pushups") {
			Workout = (await import('../workouts/workout-pushups.svelte')).default;
		}
		else if (wo_animation == "sideplank") {
			Workout = (await import('../workouts/workout-sideplank.svelte')).default;
		}
		else if (wo_animation == "jumplunges") {
			Workout = (await import('../workouts/workout-jumplunges.svelte')).default;
		}
		else if (wo_animation == "jumpsquats") {
			Workout = (await import('../workouts/workout-jumpsquats.svelte')).default;
		}
		else if (wo_animation == "mountainclimbers") {
			Workout = (await import('../workouts/workout-mountainclimbers.svelte')).default;
		}
		else if (wo_animation == "plankpushup") {
			Workout = (await import('../workouts/workout-plankpushup.svelte')).default;
		}
		else if (wo_animation == "primalstepup") {
			Workout = (await import('../workouts/workout-primalstepup.svelte')).default;
		}
    else if (wo_animation == "agilitycircles") {
			Workout = (await import('../workouts/workout-agilitycircles.svelte')).default;
		}
    else if (wo_animation == "alternatingsupermans") {
			Workout = (await import('../workouts/workout-alternatingsupermans.svelte')).default;
		}
    else if (wo_animation == "balancereaches") {
			Workout = (await import('../workouts/workout-balancereaches.svelte')).default;
		}
    else if (wo_animation == "bicycles") {
			Workout = (await import('../workouts/workout-bicycles.svelte')).default;
		}
    else if (wo_animation == "burpees") {
			Workout = (await import('../workouts/workout-burpees.svelte')).default;
		}
    else if (wo_animation == "crossbodyv") {
			Workout = (await import('../workouts/workout-crossbodyv.svelte')).default;
		}
    else if (wo_animation == "crunches") {
			Workout = (await import('../workouts/workout-crunches.svelte')).default;
		}
    else if (wo_animation == "curtsylunges") {
			Workout = (await import('../workouts/workout-curtsylunges.svelte')).default;
		}
    else if (wo_animation == "diagonallunges") {
			Workout = (await import('../workouts/workout-diagonallunges.svelte')).default;
		}
    else if (wo_animation == "divebomberpushup") {
			Workout = (await import('../workouts/workout-divebomberpushup.svelte')).default;
		}
    else if (wo_animation == "doublecrunches") {
			Workout = (await import('../workouts/workout-doublecrunches.svelte')).default;
		}
    else if (wo_animation == "hellodollies") {
			Workout = (await import('../workouts/workout-hellodollies.svelte')).default;
		}
    else if (wo_animation == "hightailpushups") {
			Workout = (await import('../workouts/workout-hightailpushups.svelte')).default;
		}
    else if (wo_animation == "jumpingjacks") {
			Workout = (await import('../workouts/workout-jumpingjacks.svelte')).default;
		}
    else if (wo_animation == "laterallunges") {
			Workout = (await import('../workouts/workout-laterallunges.svelte')).default;
		}
    else if (wo_animation == "lunges") {
			Workout = (await import('../workouts/workout-lunges.svelte')).default;
		}
    else if (wo_animation == "prisoners") {
			Workout = (await import('../workouts/workout-prisoners.svelte')).default;
		}
    else if (wo_animation == "pushuprotate") {
			Workout = (await import('../workouts/workout-pushuprotate.svelte')).default;
		}
    else if (wo_animation == "pushupspider") {
			Workout = (await import('../workouts/workout-pushupspider.svelte')).default;
		}
    else if (wo_animation == "rest") {
			Workout = (await import('../workouts/workout-rest.svelte')).default;
		}
    else if (wo_animation == "reverselungerotate") {
			Workout = (await import('../workouts/workout-reverselungerotate.svelte')).default;
		}
    else if (wo_animation == "reverselunges") {
			Workout = (await import('../workouts/workout-reverselunges.svelte')).default;
		}
    else if (wo_animation == "shadowboxing") {
			Workout = (await import('../workouts/workout-shadowboxing.svelte')).default;
		}
    else if (wo_animation == "skater") {
			Workout = (await import('../workouts/workout-skater.svelte')).default;
		}
    else if (wo_animation == "sprints") {
			Workout = (await import('../workouts/workout-sprints.svelte')).default;
		}
    else if (wo_animation == "squats") {
			Workout = (await import('../workouts/workout-squats.svelte')).default;
		}
    else if (wo_animation == "stepupsquats") {
			Workout = (await import('../workouts/workout-stepupsquats.svelte')).default;
		}
    else if (wo_animation == "surfers") {
			Workout = (await import('../workouts/workout-surfers.svelte')).default;
		}
    else if (wo_animation == "swimmers") {
			Workout = (await import('../workouts/workout-swimmers.svelte')).default;
		}
    else if (wo_animation == "tensandtwos") {
			Workout = (await import('../workouts/workout-tensandtwos.svelte')).default;
		}
    else if (wo_animation == "toetouches") {
			Workout = (await import('../workouts/workout-toetouches.svelte')).default;
		}
    else if (wo_animation == "tricepsdipandreach") {
			Workout = (await import('../workouts/workout-tricepsdipandreach.svelte')).default;
		}
    else if (wo_animation == "tricepsdips") {
			Workout = (await import('../workouts/workout-tricepsdips.svelte')).default;
		}
    else if (wo_animation == "wormwalkouts") {
			Workout = (await import('../workouts/workout-wormwalkouts.svelte')).default;
		}

    else {Workout = (await import('../workouts/workout-plank.svelte')).default;}
    }    
    
    onMount(async () => {
		await sleep(10); // simulate network delay
		loadAnimation();
    });
   
  </script>

  <style lang="scss">
    .animation
    {
	--hair:inherit;
    --pants:inherit;
    --flesh:inherit;
    --shirt:inherit;
    --cool200: #C6C8D2;
    --book: var(--cool200);
    width:100%;
    max-width: 400px;
    height: 35vh;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto;
   
}
 

  </style>

<div class="animation">
<svelte:component this={Workout} bind:isPaused bind:direction bind:rootElement>
</svelte:component>
</div>
