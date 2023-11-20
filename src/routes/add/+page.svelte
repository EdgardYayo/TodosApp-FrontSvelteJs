<script>
    import Form from "../../components/Form.svelte";
    import { onMount } from 'svelte'
    import { goto } from '$app/navigation'

    onMount(() => {
        let userData = JSON.parse(localStorage.getItem('user'))

        if(!userData || !userData.access_token){
            goto('/')
        }
    })
</script>

<main>
    <h1>Create your new Todo</h1>
    <Form></Form>
</main>

<style>
    main {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    h1 {
        font-family: monospace;
        font-style: italic;
        font-weight: 300;
        text-shadow: 1px 1px 1px tomato;
    }
</style>