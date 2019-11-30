<script>
  let newTodo = "";
  let todos = [];

  const addTodo = () => {
    if (newTodo != "") {
      const newTodoItem = {
        task: newTodo,
        checked: false
      };
      todos = [...todos, newTodoItem];
      console.log(todos);
      newTodo = "";
    }
  };

  const changeChecked = (i, checked) => {
    console.log(i, checked);
    todos[i].checked = checked;
  };

  const removeTodo = i => {
    todos.splice(i, 1);
    // update variable value to force rerender
    todos = todos;
  };
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  .todo-item {
    margin: 12px 0 12px 0;
    font-size: 24px;
  }

  .remove-btn {
    background: #ff3e00;
    color: white;
    border: none;
    padding: 2px 12px 2px 12px;
  }
</style>

<main>
  <h1>Svelte Todo</h1>
  <div>
    <input type="text" placeholder="Add Todo Item" bind:value={newTodo} />
    <button on:click={addTodo}>Add</button>
  </div>
  <div>
    {#each todos as { task, checked }, i}
      <div class="todo-item">
        <span>{i}: {task}</span>
        <input
          type="checkbox"
          {checked}
          on:change={() => changeChecked(i, !checked)} />
        <button class="remove-btn" on:click={() => removeTodo(i)}>x</button>
      </div>
    {/each}
  </div>
</main>
