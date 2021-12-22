<script>
	import {onMount} from 'svelte'
	import Header from './components/Header.svelte'
	import Instructions from './components/Instructions.svelte'
	import GoalForm from './components/GoalForm.svelte'
	import Goal from './components/Goal.svelte'
	import {fade} from 'svelte/transition'
	let newGoal = false
	let goals = []
	let url = "https://write-io.herokuapp.com/goal/"
	const getGoals = async () => {
		const response = await fetch(url)
		const data = await response.json()
		goals = data
	}
	let animate = false
	let token
	onMount(() => {
		getGoals()
		animate = true
	})
</script>
	

<style>

	@import url('https://fonts.googleapis.com/css2?family=Caveat&family=Roboto:wght@100&family=Vujahday+Script&display=swap');
    
    :global(*){
        font-family: 'Caveat', cursive;
    }

	:global(textarea){
		font-family: 'Roboto', sans-serif;
	}

	:global(button, input[type='submit']){
		background-color: white;
		color: black;
		border-radius: 10px;
		border: solid 3px black;
	}

	button {
		font-size: 2em;
	}

	main {
		text-align: center;
	}
</style>

<Header/>
<Instructions/>
<main>
{#if token}
<div></div>
{:else}
	{#if animate}
	<button transition:fade={{duration:500, delay:3000}} on:click={() => newGoal = !newGoal}>New Goal</button>
	{/if}
	{#if newGoal}
	<GoalForm url={url} method={'post'} getGoals={getGoals}/>
	{/if}
	{#each goals as item}
	<Goal goal={item} getGoals={getGoals}/>
	{/each}
{/if}
</main>
