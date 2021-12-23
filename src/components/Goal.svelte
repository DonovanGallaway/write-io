<script>
    import GoalForm from './GoalForm.svelte'
    import {fade, fly} from 'svelte/transition'
    export let goal
    export let getGoals
    $: wordCount = goal.text.split(' ').length - 1
    $: goal.goalMet = goal.wordGoal <= goal.text.split(' ').length -1
    let edit = false
    let url = "https://write-io.herokuapp.com/goal/" + goal._id
    const toggleEdit = () => {edit = !edit}

    const deleteGoal = async () => {
        await fetch(url, {
            method: "delete"
        })
        getGoals()
    }
    let done
    $: if (goal.goalMet){
        done = "green"
    } else {
        done = "red"
    }

    export let stillWriting = false

    const saveGoal = async () => {
		await fetch(url, {
			method: "put",
			headers: {
				"Content-Type": "application/json"
			},
			body: JSON.stringify(goal)
		})
        getGoals()
        stillWriting = false        
	}

    let editButton
    $: if (edit){
        editButton = "Cancel"
    } else {
        editButton = "Edit Goal"
    }

</script>

<style>
    textarea {width: 100%; height: 300px}

    .data{
        display: flex;
        justify-content: center;
    }

    .data > * {
        margin: 1em;
    }

    #goal-met{
        color: var(--done)
    }

    .goal {
        width: 50%;
        margin: auto;
    }

    h4{
        font-size: 1.5em;
    }

    button{
        font-size: 1.5em;
    }

    .keep-writing{
        background-color: rgb(190, 252, 190);
    }

    .delete-btn{
        background-color: rgb(253, 201, 201)
    }
</style>

<div transition:fade={{duration:1000}} class='goal'>
{#if !edit}
<div class="data">
    <h4>Username: {goal.username}</h4>
    <h4>Word Goal: {goal.wordGoal}</h4>
    <h4 id="goal-met" style="--done: {done}">Word Count: {wordCount}</h4>
</div>
{:else}
    <GoalForm url={url} formData={goal} method={'put'} getGoals={getGoals} toggleEdit={toggleEdit}/>   
{/if}

{#if stillWriting}
<textarea out:fly={{x: 1000, duration:1000}} in:fly={{x: 1000, duration:1000,delay: 1000}} bind:value={goal.text}/>
<div out:fly={{x: 1000, duration:1000}} in:fly={{x: 1000, duration:1000,delay: 1000}}>
<button on:click={saveGoal}>Save</button>
<button on:click={toggleEdit}>{editButton}</button>
<button class="delete-btn" on:click={deleteGoal}>Delete Goal</button>
</div>
{:else}
<p out:fly={{x: 1000, duration:1000}} in:fly={{x: 1000, duration:1000,delay: 1000}}>{goal.text}</p>
<div out:fly={{x: 1000, duration:1000}} in:fly={{x: 1000, duration:1000,delay: 1000}}>
<button class='keep-writing' on:click={() => {stillWriting = true}}>Keep Writing!</button>
<button class='delete-btn' on:click={deleteGoal}>Delete Goal</button>
</div>
{/if}
</div>