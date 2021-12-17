<script>
    export let todos;
    export let select;
    export let destroy;
</script>

<div>
    <ul>
        {#each todos as todo}
        <li>
            <h3 on:click={() => select(todo)}>{todo.reminder} - {todo.completed}</h3>
            <button on:click={() => destroy(todo)}>Delete</button>
        </li>

        {/each}
    </ul>
    
</div>