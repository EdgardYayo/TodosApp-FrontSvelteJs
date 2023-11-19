<script>
    import axios from 'axios'
    import { goto } from '$app/navigation'
    
    let username = ''
    let password = ''

    const handleSubmit = async () => {

        const formData = new FormData()
        formData.append('username', username)
        formData.append('password', password)

        const request = await axios.post('http://localhost:8000/auth/token', formData)
        const response = await request.data
        if(response.access_token){
            localStorage.setItem('user', JSON.stringify(response))
            goto('/todos')
        }
    }

</script>

<main>
    <h1>Log in</h1>
    <form on:submit|preventDefault={handleSubmit}>
        <label>
            Username
            <input type="text" bind:value={username} />
        </label>
    <label>
        Password
        <input type="password" bind:value={password} />
    </label>
    <button type="submit">Enter</button>
    <button><a href="/sign_up">Sign Up</a></button>
</form>
</main>

<style>
    main, form {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
    }

    form {
        gap: 10px;
        border: 1px solid black;
        border-radius: 10px;
        padding: 10px;
    }

    form, label, h1, button {
        font-family: monospace;
        font-weight: 300;
    }

    button {
        border-radius: 5px;
        background-color: tomato;
        outline: none;
        border: none;
        padding: 5px;
        transition: all 300ms ease-in-out;
    }

    button:hover {
        width: 150px;
        text-decoration: underline;
    }

    a {
        text-decoration: none;
        color: black;
    }

    h1 {
        font-style: italic;
        text-shadow: 1px 1px 1px tomato;
    }

    input {
        border-radius: 15px;
        padding: 5px;
        outline: none;
    }

    input:focus {
        border-color: tomato;
    }
</style>