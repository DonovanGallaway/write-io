<script>
    import GoalForm from './GoalForm.svelte'
    export let goal
    export let getGoals
    $: wordCount = goal.text.split(' ').length - 1
    $: goal.goalMet = goal.wordGoal <= goal.text.split(' ').length -1
    let edit = false
    let url = "https://write-io.herokuapp.com/goal/" + goal._id
    const toggleEdit = () => {edit = !edit}

    const deleteGoal = () => {
        fetch(url, {
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

    let stillWriting = true

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
    textarea {width: 50%; height: 300px}

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
</style>

<div class='goal'>
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
<textarea bind:value={goal.text}/>
<div>
<button on:click={saveGoal}>Save</button>
<button on:click={toggleEdit}>{editButton}</button>
<button on:click={deleteGoal}>Delete Goal</button>
</div>
{:else}
<p>{goal.text}</p>
<div>
<button on:click={() => {stillWriting = true}}>Edit</button>
<button on:click={toggleEdit}>{editButton}</button>
<button on:click={deleteGoal}>Delete Goal</button>
</div>
{/if}
</div>