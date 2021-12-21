<script>
	import {onMount} from 'svelte'
	import Header from './components/Header.svelte'
	import Instructions from './components/Instructions.svelte'
	import GoalForm from './components/GoalForm.svelte'
	import Goal from './components/Goal.svelte'
	let newGoal = false
	let goals = []
	let url = "https://write-io.herokuapp.com/goal/"
	const getGoals = async () => {
		const response = await fetch(url)
		const data = await response.json()
		goals = data
	}
	onMount(() => {
		getGoals()
	})
	
</script>

<Header/>
<Instructions/>
<button on:click={() => newGoal = !newGoal}>New Goal</button>
{#if newGoal}
<GoalForm url={url} method={'post'} getGoals={getGoals}/>
{/if}
{#each goals as item}
<Goal goal={item} getGoals={getGoals}/>
{/each}
