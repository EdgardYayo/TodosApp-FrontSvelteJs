<script>
    import axios from "axios";

    let username = ''
    let firstName = ''
    let lastName = ''
    let email = ''
    let password = ''

    const handleSubmit = async () => {
        let payload = {
            username,
            firstName,
            lastName,
            email,
            password,
            role: 'Client'
        }

        const request = await axios.post('/auth/sign_up', payload)
        const response = await request.data
        console.log(response);
    }

</script>

<main>
    <h1>Sign up</h1>
    <form on:submit|preventDefault={handleSubmit}>
        <label>
            Username
            <input type="text" bind:value={username}  />
        </label>
        <label>
            First name
            <input type="text" bind:value={firstName}  />
        </label>
        <label>
            Last name
            <input type="text" bind:value={lastName} />
        </label>
        <label>
            Email
            <input type="email" bind:value={email} />
        </label>
        <label>
            Password
            <input type="password" bind:value={password} />
        </label>
    <button type="submit">Create user</button>
    <button><a href="/">Log in</a></button>
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