<script>
    import {CircleIcon, CheckCircleIcon, EditIcon, Trash2Icon } from 'svelte-feather-icons' 
    import {fly} from 'svelte/transition'
    export let todo ;
    export let activeEditTodo;

    import {createEventDispatcher} from 'svelte'
    const disptch = createEventDispatcher()
    const handelDelete = () => {
        disptch('deleteTodo',todo.id)
    }
    const handelEdit = () => {
        disptch('editTodo',todo)
    }

    const handleToggleTodo = () => {
        disptch('toggleTodo', todo.id)
    }
 </script>

<div class="todos-todo" class:done = {todo.done} in:fly={{x:100, duration:400}} out:fly={{x:-100, duration:400}} >
    <div class="todos-todo_icon" on:click={handleToggleTodo}>
        {#if todo.done}
           <CheckCircleIcon />
        {:else}
            <CircleIcon />
        {/if}
    </div>
    <div class="todos-todo_text">{todo.title}</div>
    {#if !activeEditTodo}
    <div class="todos-todo_cta">
        <div class="todos-todo_cta-edit" on:click={handelEdit}>
            <EditIcon size="20" />
        </div>
        <div class="todos-todo_cta-delete" on:click={handelDelete}>
            <Trash2Icon size="20" />
        </div>
    </div>
    {/if}
</div>