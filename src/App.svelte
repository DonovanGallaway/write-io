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
		goals = data.reverse()
	}
	let animate = false
	let token

	const toggleNew = () => {
		newGoal = !newGoal
	}
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
	{#if animate}
		<button transition:fade={{duration:2000, delay:1000}} on:click={toggleNew}>New Goal</button>
	{/if}
	{#if newGoal}
		<GoalForm url={url} method={'post'} getGoals={getGoals} toggleNew={toggleNew}/>
	{/if}
	{#each goals as item}
		{#if item.text}
			<div transition:fade={{duration:2000, delay:1000}}>
			<Goal goal={item} getGoals={getGoals}/>
		</div>
		{:else}
			<Goal goal={item} getGoals={getGoals} stillWriting={true}/>
		{/if}
	{/each}
</main>
