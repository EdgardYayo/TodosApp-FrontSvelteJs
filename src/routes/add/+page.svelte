<script>
    import Form from "../../components/Form.svelte";
</script>

<style>
    main {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    button {
        width: 100px;
        padding: 5px;
        border-radius: 10px;
        outline: none;
        border: none;
        background: black;
    }
</style>

<main>
    <h2>Create your new Todo</h2>
    <Form></Form>
</main>