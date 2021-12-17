<script>
    export let reminder
    export let completed
    export let _id
    export let action
    export let create
    export let update

    //functions
    const handleSubmit = (event) => {
        event.preventDefault()
        if(action === "create"){
            create({reminder, completed})
        }
        if(action === "update"){
            update({reminder, _id, completed})
        }
    }

</script>

<div>
    <form on:submit={handleSubmit}>
        <input type="text" bind:value={reminder}>
        <input type="checkbox" bind:checked={completed}>
        <input type="submit">
    </form>
    
</div>