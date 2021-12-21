<script>
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

{#if method=='post'}
<form on:submit|preventDefault={addGoal}>
    <label for='username'>Username: 
        <input type='text' name='username' bind:value={formData.username}/>
    </label>
    <label for='word goal'>Word Goal: 
        <input type='number' name='wordGoal' bind:value={formData.wordGoal}/>
    </label>
    <input type='submit' value='Add Goal'/>
</form>

{:else}
<form on:submit|preventDefault={editGoal}>
    <label for='username'>Username: 
        <input type='text' name='username' bind:value={formData.username}/>
    </label>
    <label for='word goal'>Word Goal: 
        <input type='number' name='wordGoal' bind:value={formData.wordGoal}/>
    </label>
    <input type='submit' value='Edit Goal'/>
</form>
{/if}