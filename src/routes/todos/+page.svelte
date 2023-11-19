<script>
    import { onMount } from "svelte";
    import axios from "axios"

    let todos = []

    onMount(async () => {
        try {
            const userToken = JSON.parse(localStorage.getItem('user')).access_token
            const request = await fetch("http://localhost:8000/", {
                headers: {
                'Authorization': `Bearer ${userToken}` // Replace yourAuthToken with the actual token
            }
            });
            const response = await request.json()
            console.log(response);
            todos = response
        } catch (error) {
            console.log(error);
        }
    })



    const deleteTodo = async (todo_id) => { 
        try {
           await axios.delete("http://localhost:8000/todo/delete/" + todo_id)
           todos = todos.filter(todo => todo.id !== todo_id)
        } catch (error) {
            console.log(error);
        }
    }

    const tagImportance = (priority) => {
        let prior = {
            1: "Not important",
            2: "Need to be atended",
            3: "Important",
            4: "Very Important",
            5: "Crucial",
        }

        return prior[priority];
    }
</script>

<main>
    <h2>Your todos</h2>
    <table>
        <thead>
            <tr>
                <td>Title</td>
                <td>Description</td>
                <td>Priority</td>
                <td>Complete</td>
                <td>Delete</td>
            </tr>
        </thead>
        <tbody>
            {#each todos as todo }
                <tr>
                    <td>{todo.title}</td>
                    <td>{todo.description}</td>
                    <td>{tagImportance(todo.priority)}</td>
                    <td>{todo.complete ? "Complete" : "Pending"}</td>
                    <td><button on:click={() => deleteTodo(todo.id)}>X</button></td>
                </tr>
            {/each}
        </tbody>
    </table>
</main>

<style>
    main {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        min-height: 70vh;
    }

    table {
        border: 1px solid black;
        padding: 3px;
    }

    tr {
        border: 1px solid black;
        padding: 10px;
    }

    button {
        color: red;
    }
</style>