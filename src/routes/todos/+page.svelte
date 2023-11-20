<script>
    import { onMount } from "svelte";
    import axios from "axios"

    let todos = []

    const fetchTodos = async () => {
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
    }

    onMount(fetchTodos)



    const deleteTodo = async (todo_id) => { 
        try {
           const userToken = JSON.parse(localStorage.getItem('user')).access_token
           axios.defaults.headers.common['Authorization'] = 'Bearer ' + userToken;
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

    const completeTodo = async (todo_id) => {
        try {
            const userToken = JSON.parse(localStorage.getItem('user')).access_token
            axios.defaults.headers.common['Authorization'] = 'Bearer ' + userToken;
            await axios.patch("http://localhost:8000/todo/complete/" + todo_id)
            fetchTodos()
        } catch (error) {
            console.log(error);
        }
        
    }
</script>

<main>
    <h1>Your todos</h1>
    <table>
        <thead>
            <tr>
                <td>Title</td>
                <td>Description</td>
                <td>Priority</td>
                <td>Complete</td>
                <td>Delete</td>
                <td>Mark as complete</td>
            </tr>
        </thead>
        <tbody>
            {#each todos as todo }
                <tr>
                    <td>{todo.title}</td>
                    <td>{todo.description}</td>
                    <td>{tagImportance(todo.priority)}</td>
                    <td>{todo.complete ? "✅" : "❌"}</td>
                    <td><button on:click={() => deleteTodo(todo.id)}>🚮</button></td>
                    <td><button on:click={() => completeTodo(todo.id)}>🆗</button></td>
                </tr>
            {/each}
        </tbody>
    </table>
    <button class="addTodoBtn">
        <a href="/add">Add Todo</a>
    </button>
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
        padding: 20px;
        border-radius: 10px;
        font-family: monospace;
        font-weight: 300;
        
    }

    thead {
        font-weight: 900;
    }

    tr {
        border: 1px solid black;
        padding: 10px;
    }

    td > button {
        background-color: transparent;
        cursor: pointer;
        border: none;
    }

    td {
        text-align: center;
        padding: 5px;
    }

    .addTodoBtn {
        margin-block-start: 10px;
        border-radius: 5px;
        background-color: tomato;
        outline: none;
        border: none;
        padding: 5px;
        transition: all 300ms ease-in-out;
    }

    .addTodoBtn > a {
        color: black;
        text-decoration: none;
    }

    .addTodoBtn:hover {
        width: 150px;
        text-decoration: underline;
    }
    
    h1 {
        font-family: monospace;
        font-style: italic;
        font-weight: 300;
        text-shadow: 1px 1px 1px tomato;
    }
</style>