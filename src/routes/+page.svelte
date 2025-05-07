<script lang="ts">
    import { onMount } from 'svelte';
  
    interface Todo {
      text: string;
      checked: boolean;
    }
  
    let todos: Todo[] = [
      { text: 'Hit the gym', checked: false },
      { text: 'Pay bills', checked: true },
      { text: 'Meet George', checked: false },
      { text: 'Buy eggs', checked: false },
      { text: 'Read a book', checked: false },
      { text: 'Organize office', checked: false }
    ];
  
    let newTodo: string = '';
  
    function addTodo() {
      if (newTodo.trim()) {
        todos = [...todos, { text: newTodo, checked: false }];
        newTodo = '';
      }
    }
  
    function toggleChecked(index: number) {
      todos = todos.map((todo, i) =>
        i === index ? { ...todo, checked: !todo.checked } : todo
      );
    }
  
    function removeTodo(index: number) {
      todos = todos.filter((_, i) => i !== index);
    }
  </script>
  
  <div class="header">
    <h2>My To Do List</h2>
    <input
      bind:value={newTodo}
      type="text"
      placeholder="Title..."
      on:keydown={(e) => e.key === 'Enter' && addTodo()}
    />
    <button on:click={addTodo} class="addBtn">Add</button>
  </div>
  
  <ul id="myUL">
    {#each todos as { text, checked }, index}
      <li class:checked={checked}>
        <button class="task {checked ? 'checked' : ''}" on:click={() => toggleChecked(index)}>{text}</button>
        <button class="close" on:click={(e) => { e.stopPropagation(); removeTodo(index); }} aria-label="Remove">&times;</button>
      </li>
    {/each}
  </ul>
  
  <style>
    * {
      box-sizing: border-box;
    }
  
    ul {
      margin: 0;
      padding: 0;
    }
  
    ul li {
      position: relative;
      padding: 0;
      list-style: none;
      margin-bottom: 5px;
    }
  
    .task {
      cursor: pointer;
      width: 100%;
      padding: 12px 8px 12px 40px;
      background: #eee;
      font-size: 18px;
      text-align: left;
      transition: 0.2s;
      border: none;
    }
  
    ul li:nth-child(odd) .task {
      background: #f9f9f9;
    }
  
    ul li:nth-child(odd).checked .task {
      background: #888;  /* темніший фон для непарних елементів з "checked" */
    }
  
    .task:hover {
      background: #ddd;
    }
  
    .task.checked {
      background: #888;
      color: #fff;
      text-decoration: line-through;
    }
  
    .close {
      position: absolute;
      right: 0;
      top: 0;
      padding: 12px 16px;
      background: transparent;
      border: none;
      cursor: pointer;
      color: #888;
      font-size: 18px;
    }
  
    .close:hover {
      background-color: #f44336;
      color: white;
    }
  
    .header {
      background-color: #f44336;
      padding: 30px 40px;
      color: white;
      text-align: center;
    }
  
    .header:after {
      content: "";
      display: table;
      clear: both;
    }
  
    input {
      margin: 0;
      border: none;
      border-radius: 0;
      width: 75%;
      padding: 10px;
      float: left;
      font-size: 16px;
    }
  
    .addBtn {
      padding: 10px;
      width: 25%;
      background: #d9d9d9;
      color: #555;
      float: left;
      text-align: center;
      font-size: 16px;
      cursor: pointer;
      transition: 0.3s;
      border-radius: 0;
    }
  
    .addBtn:hover {
      background-color: #bbb;
    }
  
    ul li.checked {
      background: #888;
      color: #fff;
      text-decoration: line-through;
    }
  </style>
  