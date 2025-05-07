
<script>
    import { onMount } from 'svelte';
    let todos = [
      { text: 'Hit the gym', checked: false },
      { text: 'Pay bills', checked: true },
      { text: 'Meet George', checked: false },
      { text: 'Buy eggs', checked: false },
      { text: 'Read a book', checked: false },
      { text: 'Organize office', checked: false }
    ];
  
    let newTodo = '';
  
    function addTodo() {
      if (newTodo.trim()) {
        todos = [...todos, { text: newTodo, checked: false }];
        newTodo = '';
      }
    }
  
    function toggleChecked(index) {
      todos = todos.map((todo, i) =>
        i === index ? { ...todo, checked: !todo.checked } : todo
      );
    }
  
    function removeTodo(index) {
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
        <span on:click={() => toggleChecked(index)}>{text}</span>
        <span class="close" on:click={(e) => { e.stopPropagation(); removeTodo(index); }}>&times;</span>
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
      cursor: pointer;
      position: relative;
      padding: 12px 8px 12px 40px;
      background: #eee;
      font-size: 18px;
      transition: 0.2s;
      -webkit-user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;
      user-select: none;
    }
  
    ul li:nth-child(odd) {
      background: #f9f9f9;
    }
  
    ul li:hover {
      background: #ddd;
    }
  
    ul li.checked {
      background: #888;
      color: #fff;
      text-decoration: line-through;
    }
  
    ul li.checked::before {
      content: '';
      position: absolute;
      border-color: #fff;
      border-style: solid;
      border-width: 0 2px 2px 0;
      top: 10px;
      left: 16px;
      transform: rotate(45deg);
      height: 15px;
      width: 7px;
    }
  
    .close {
      position: absolute;
      right: 0;
      top: 0;
      padding: 12px 16px;
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
  </style>
  


