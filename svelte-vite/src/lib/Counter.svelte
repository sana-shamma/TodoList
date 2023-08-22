<script>
  import {createEventDispatcher} from 'svelte'
  const disptch = createEventDispatcher()
  export let user;
  let count = 0
  const increment = () => {
    count += 1

    disptch('changeName','sara')
  }
  let list = ['Sana','Salwa']

  const fetchTodos= async () => {
    const res = await fetch ('https://jsonplaceholder.typicode.com/todos?_limit=5')
    const data = await res.json()
    console.log(data)

    if (res.ok){ list = data}
    else {throw new Error('error in api')}
  }

  fetchTodos()
</script>

<button on:click={increment}>
  count is {count}
  <p>{user}</p>

  {#await fetchTodos}
  <p>loading</p>
  {:then data}
  {#each list as x (x) }
  <p>{x}</p>
  {/each}
  {:catch error}
  <p>{error}</p>
  {/await}
</button>
