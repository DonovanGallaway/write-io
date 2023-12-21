<script>
    let formData = {
        username: "",
        password: ""
    }

    const url = "https://nanowrimo-backend-ed979ddf8fb7.herokuapp.com/auth/signup"

    const handleSubmit = async (formData) => {
        await fetch(url, {
            method: "post",
            headers: {
                "Content-Type": "application/json"
            },
            body: JSON.stringify({username, password})
        })
    }
</script>

<form on:submit={handleSubmit}>
    <label for="username">Username: 
        <input type='text' name='username' bind:value={formData.username}/>
    </label>
    <label for="password">Password
        <input type='text' name='password' bind:value={formData.password}/>
    </label>
    <input type='submit' value='Sign Up'/>
</form>