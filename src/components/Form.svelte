<script>

</script>

<style>
    form {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 20px;
        border: 2px black solid;
        padding: 20px;
        border-radius: 20px;
        min-width: 300px;
    }

    label {
        color: black;
        font-weight: bold;
    }

    button {
        width: 100px;
        padding: 5px;
        border-radius: 10px;
        outline: none;
        border: none;
        background: black;
        color: white;
    }
    
    a {
        color: white;
        text-decoration: none;
    }

</style>


<form method="post">
    <label>
        Title
        <input name="title" id="title" placeholder="title"/>
    </label>
    <label>
        Description
        <input name="description" id="description" placeholder="description"/>
    </label>
    <label>
        Priority
        <input name="priority" id="priority" placeholder="pritority"/>
    </label>
    <label>
        Complete
        <input name="complete" id="complete" placeholder="complete"/>
    </label>
    <button type="submit">Save</button>
    <button><a href="/">Back</a></button>
</form>