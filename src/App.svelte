<script>
  import {onMount} from "svelte"
  import Display from "./components/Display.svelte"
  import Form from "./components/Form.svelte"

  const url = "http://localhost:10000/todos"

  // state
  let showForm = false 
  let reminder = ""
  let completed = false
  let _id = ""
  let todos = []
  let action = "create"

  //functions
  const getTodos = async () => {
    const response = await fetch(url)
    const data = await response.json()
    todos = data
  }

  //show form
  const toggleForm = () => {
    showForm = !showForm
  }

  const resetState = () => {
    reminder = ""
    completed = false
    showForm = false
    _id = ""
    action="create"
    getTodos()
  }

  //create todo
  const createTodos = async (todo) => {
    await fetch(url, {
      method: "post",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify(todo)
    })
    resetState()
  }

const selectTodoToUpdate = (todo) => {
  reminder = todo.reminder
  completed = todo.completed
  _id = todo._id
  action = "update"
  showForm = true
}

const updateTodos  = async (todo) => {
    await fetch(url +`/${todo._id}`, {
      method: "put",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify(todo)
    })
    resetState()
  } 

const deleteTodos  = async (todo) => {
    await fetch(url +`/${todo._id}`, {
      method: "delete",
    })
    resetState()
  } 



//Life cycle
onMount(() => { getTodos() })

</script>

<main>
  <h1>MY TODO'S</h1>
  <button on:click={toggleForm}>Create to do</button>
  <Display 
    todos={todos} 
    select={selectTodoToUpdate}
    destroy={deleteTodos}
  />
  {#if showForm}
  <Form
    reminder={reminder}
    completed={completed}
    _id={_id}
    action={action}
    create={createTodos}
    update={updateTodos}
  />
  {/if}
</main>

<style>
  
</style>
