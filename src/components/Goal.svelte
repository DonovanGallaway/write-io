<script>
    import GoalForm from './GoalForm.svelte'
    export let goal
    export let getGoals
    $: wordCount = goal.text.split(' ').length - 1
    $: goal.goalMet = goal.wordGoal <= goal.text.split(' ').length
    let edit = false
    let url = "https://write-io.herokuapp.com/goal/" + goal._id
    const toggleEdit = () => {edit = !edit}

    const deleteGoal = () => {
        fetch(url, {
            method: "delete"
        })
        getGoals()
    }

</script>

<style>
    textarea {width: 50%; height: 300px}
</style>

{#if !edit}
    <h4>Username: {goal.username}</h4>
    <h4>Word Goal: {goal.wordGoal}</h4>
    <h4>Word Count: {wordCount}</h4>
    <h4>{goal._id}</h4>
    {#if goal.goalMet}
    <h4>Goal Met!</h4>
    {:else}
    <h4>Goal Not met...</h4>
    {/if}
{:else}
    <GoalForm url={url} formData={goal} method={'put'} getGoals={getGoals} toggleEdit={toggleEdit}/>   
{/if}
<button on:click={toggleEdit}>Edit Goal</button>
<button on:click={deleteGoal}>Delete Goal</button>
<textarea bind:value={goal.text}/>