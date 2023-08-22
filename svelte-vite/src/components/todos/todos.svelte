<script>
    import Todo from "./todo.svelte";
    export let todos =[] ;
    export let activeEditTodo;

    $: activeTodos= activeEditTodo? [activeEditTodo]:todos
</script>

<div class="tods-list">
    {#each activeTodos as todo (todo.id) }
    <Todo {todo} activeEditTodo={activeEditTodo} on:deleteTodo on:editTodo on:toggleTodo/>
    {/each }
    {#if todos.length === 0}
    <h3 class="no-todos">لا يوجد مهام حاليا</h3>
    {/if}
</div>