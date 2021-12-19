<script>
import { onMount } from 'svelte';

    import {fade,fly} from 'svelte/transition'
    let animate
    onMount(() => {
        animate = true
    })
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Vujahday+Script&display=swap');
    
    *{
        font-family: 'Vujahday Script', cursive;
    }
    nav {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
    }

    h1 {
        font-size: 3em;
        margin-left: 1.5em;
    }

    .logo{
        width: 36px;
        margin-left: 1.5em;
        margin-right: 1.5em;
    }

    .logos {
        margin-right: 3em;
    }
</style>

<nav>
{#if animate}
    <h1 transition:fade={{duration:1000}}>NaNoWriM.io</h1>
    <div transition:fly={{y:1000,duration:2000,delay:1000}} class="logos">
        <a href='https://github.com/DonovanGallaway'><img class="logo" src='img/github-logo.png' alt='github'/></a>
        <a href='https://www.linkedin.com/in/donovan-gallaway/'><img class="logo" src='/img/linkedin-logo.png' alt='linkedin'/></a>
    </div>
{/if}
</nav>