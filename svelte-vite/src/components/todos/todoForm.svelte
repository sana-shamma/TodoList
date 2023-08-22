<script>
   import {CircleIcon} from 'svelte-feather-icons' 

   export let activeEditTodo;
   export let isFilter;
   let value = '';
   import {createEventDispatcher} from 'svelte'
    const disptch = createEventDispatcher()

   const handleAddTodo = () => {
    if (!value.trim()){
        return
    }
    disptch('addTodo',value.trim())
    value=''
   }

   const editChange = () => {
    if (activeEditTodo){
        console.log(activeEditTodo.title)
        value = activeEditTodo.title
    }
   }

   const handleFilter =() =>{
    disptch('filter')
   }
   $:activeEditTodo, editChange()
</script>

<div class="todos-form">
    <div class="todos-form_icon" class:active={isFilter} on:click={handleFilter}>
        <CircleIcon/>
    </div>
    <div class="todos-form_form">
        <input bind:value={value} type="text" placeholder="أضف مهمة جديدة ..." />
    </div>
    <div class="todos-form_sumbit" on:click = {handleAddTodo}>
        <button class="btn" disabled={!value.trim()}>
            {activeEditTodo ? 'تعديل':'إضافة'}
            </button>
    </div>
</div>