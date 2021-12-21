<script>
    import {fade, fly, blur, slide, scale, draw, crossfade} from 'svelte/transition'

    export let formData = {
        username: "",
        wordGoal: 0,
        goalMet: false,
        text: ""
    }

    // $: console.log(formData)

    export let url
    export let getGoals
    export let method = 'post'
    export let toggleEdit

    const addGoal = async () => {
		await fetch(url, {
			method: "post",
			headers: {
				"Content-Type": "application/json"
			},
			body: JSON.stringify(formData)
		})
        getGoals()        
	}

    const editGoal = async () => {
		await fetch(url, {
			method: "put",
			headers: {
				"Content-Type": "application/json"
			},
			body: JSON.stringify(formData)
		})
        toggleEdit()
        getGoals()        
	}

</script>

<style>
    h4{
        font-size: 2em;
        margin: .5em;
    }
</style>

{#if method=='post'}
<form transition:slide on:submit|preventDefault={addGoal}>
    <label for='username'><h4>Username:</h4>
        <input type='text' name='username' bind:value={formData.username}/>
    </label>
    <label for='word goal'><h4>Word Goal: </h4>
        <input type='number' name='wordGoal' bind:value={formData.wordGoal}/>
    </label>
    <input type='submit' value='Add Goal'/>
</form>

{:else}
<form on:submit|preventDefault={editGoal}>
    <label for='username'><h4>Username:</h4>
        <input type='text' name='username' bind:value={formData.username}/>
    </label>
    <label for='word goal'><h4>Word Goal: </h4>
        <input type='number' name='wordGoal' bind:value={formData.wordGoal}/>
    </label>
    <input type='submit' value='Edit Goal'/>
</form>
{/if}