<script>
    import {onMount} from 'svelte'
    import {fade} from 'svelte/transition'
    let instructions = false
    onMount(()=> {
        instructions = true
    })
    let showState = "Hide"
    const hideInstruction = () => {
        instructions = !instructions
        if (instructions){
            showState = "Hide"
        } else {
            showState = "Show"
        }
    }
</script>

<style>
    div {
        width: 50vw;
        margin: auto;
    }

    p {
        font-size: 2em;
    }

    span{
        color: blue;
    }
</style>

<div>
{#if instructions}
    <div in:fade={{duration: 1000, delay:1000}} out:fade={{duration:500}} on:click={hideInstruction}>
        <p><i>Welcome to the (very) unofficial "National Novel Writing Month App," affectionately dubbed "NaNoWriM.io" after the abbreviation for the event ("NaNoWriMo").<br/><br/>
        The purpose of the app is to help you track and meet your quotas for NaNoWriMo or your writing in general, making sure you have a space to track your word counts and words. It should be noted that this assumes a writing method involving a computer and an actual desire to write more and set quotas. After all, cheaters never prosper and it's hard to help someone who writes with pen and paper by using word processing tools...<br/><br/>
        Anyway! Hope you enjoy! <span>(click to hide)</span></i></p>
    </div>
    {:else}
<div></div>
{/if}


</div>