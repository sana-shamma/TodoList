<script>
    import TodoForm from "../components/todos/todoForm.svelte";
    import Todos from "../components/todos/todos.svelte";

    let todos = [
        {id:1, title: "مشاهدة كورس", done:false},
        {id:2, title: "شراء منتجات", done:true},
        {id:3, title: "كتابة كود", done:false},
        {id:4, title: "قراءة كتاب" , done:true},
    ]

    let isFilter = false

    let activeEditTodo = null

    const deleteTodo = (e) => {
        const id = e.detail
        todos = todos.filter(t => t.id !=id)
    }

    const addTodo = (e) =>{
        const title = e.detail
        const id = new Date().getTime()
        if(!activeEditTodo){
            todos= [{title, id, done:false}, ...todos]
        }
        else{
            todos = todos.map(t => {
                if (activeEditTodo.id ===t.id){
                    t.title = title
                }
                return t
            })
            activeEditTodo = null
        }
    }

    const editTodo = (e) => {
        activeEditTodo=e.detail
    }

    const toggleTodo = (e) => {
        if (activeEditTodo){
            return
        }
        const id = e.detail
        todos = todos.map(t=>{
            if(t.id === id){
                t.done = ! t.done
            }
            return t
        })
    }

    const filter = () => {
        isFilter = !isFilter
    }

    $:allTodos = isFilter ? todos.filter(t=>!t.done):todos
</script>

<main>
<div class="container">
    <div class="todos">
        <TodoForm isFilter={isFilter} activeEditTodo={activeEditTodo} on:addTodo={addTodo} on:filter={filter}/>
        <Todos todos={allTodos} activeEditTodo={activeEditTodo} on:deleteTodo={deleteTodo} on:editTodo={editTodo} on:toggleTodo={toggleTodo} />
    </div>
</div>    
</main>