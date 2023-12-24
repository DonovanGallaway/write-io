<script>

    export let login

    const base_url = "https://nanowrimo-backend-ed979ddf8fb7.herokuapp.com/auth"

    const url = login ? base_url + "/login" : base_url + "/signup"

    let password_matches = true

    let formData = {
        username: "",
        password: ""
    }

    let confirm_password

    const handleSubmit = async () => {
        if (formData.password != confirm_password){
            password_matches = false
            return
        }
        else {
            password_matches = true
        }
        await fetch(url, {
            method: "post",
            headers: {
                "Content-Type": "application/json"
            },
            body: JSON.stringify(formData)
        })
    }
</script>

<form on:submit={handleSubmit}>
    <label for="username">Username: 
        <input type='text' name='username' bind:value={formData.username}/>
    </label>
    <label for="password">Password
        <input type='password' name='password' bind:value={formData.password}/>
    </label>
    {#if login}
        <label for="confirm password">Confirm Password
            <input type="password" name="confirm_password" bind:value={confirm_password}/>
        </label>
        {#if !password_matches}
            <p>Passwords do not match</p>
        {/if}
    {/if}
    <input type='submit' value='Sign Up'/>
</form>