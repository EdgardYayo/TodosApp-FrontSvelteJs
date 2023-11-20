<script>
    import axios from "axios";
    import { goto } from '$app/navigation';

    let title = ''
    let description = ''
    let priority = 0

    const handleSubmit = async () => {
        let userData = JSON.parse(localStorage.getItem('user'))
        
        if (userData && userData.access_token) {
            axios.defaults.headers.common['Authorization'] = 'Bearer ' + userData.access_token;
            console.log(axios.defaults.headers.common);

        } else {
            alert('You are not authenticated')
            goto('/')
        }

        let newTodo = {
            title,
            description,
            priority,
            complete: false
        }

        const request = await axios.post('http://localhost:8000/todo/new', newTodo)
        const response = await request.data

        if(response === null){
            goto('/todos')
        } else {
            alert('Somenthing went wrong try again');
        }

        
    }


</script>


<form on:submit|preventDefault={handleSubmit}>
    <label>
        Title
        <input type="text" minlength="3" maxlength="100" bind:value={title} placeholder="title"/>
    </label>
    <label>
        Description
        <textarea type="text" minlength="6" maxlength="200" bind:value={description} placeholder="description"/>
    </label>
    <label>
        Priority
        <input type="number" min="1" max="5" bind:value={priority} placeholder="pritority"/>
    </label>
    <button type="submit">Save</button>
    <button><a href="/todos">Back</a></button>
</form>

<style>
    form {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 10px;
        border: 1px black solid;
        padding: 10px;
        border-radius: 10px;
        min-width: 300px;
        font-family: monospace;
        font-weight: 300;
    }

    label {
        color: black;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 10px;
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

    input, textarea {
        border-radius: 15px;
        padding: 5px;
        outline: none;
    }

    input:focus, textarea:focus {
        border-color: tomato;
    }

</style>