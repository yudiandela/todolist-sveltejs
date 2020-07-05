<script>
  let todos = [];
  let todoText = "";
  let todo = "";

  function addTodos() {
    if (todoText !== "") {
      todo = {
        id: todos.length + 1,
        text: todoText,
        class: false
      };
      todos = [...todos, todo];
      todoText = "";
    } else {
      alert("Anda tidak memasukkan teks apapun");
    }
  }

  function removeItemOnce(array, value) {
    let index = array.indexOf(value);
    if (index > -1) {
      array.splice(index, 1);
      todos = array;
    }
  }

  function changeClass(array, value) {
    let index = array.indexOf(value);
    if (index > -1) {
      array[index].class = !array[index].class;
      todos = array;
    }
  }
</script>

<style>
  main {
    margin: 0 auto;
    padding: 1em;
    max-width: 640px;
  }

  /* Include the padding and border in an element's total width and height */
  * {
    box-sizing: border-box;
  }

  /* Remove margins and padding from the list */
  ul {
    margin: 0;
    padding: 0;
  }

  /* Style the list items */
  ul li {
    cursor: pointer;
    position: relative;
    padding: 12px 8px 12px 40px;
    list-style-type: none;
    background: #eee;
    font-size: 18px;
    transition: 0.2s;

    /* make the list items unselectable */
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
  }

  /* Set all odd list items to a different color (zebra-stripes) */
  ul li:nth-child(odd) {
    background: #f9f9f9;
  }

  /* Darker background-color on hover */
  ul li:hover {
    background: #ddd;
  }

  /* When clicked on, add a background color and strike out text */
  ul li.checked {
    background: #888;
    color: #fff;
    text-decoration: line-through;
  }

  /* Add a "checked" mark when clicked on */
  ul li.checked::before {
    content: "";
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

  /* Style the close button */
  .close {
    position: absolute;
    right: 0;
    top: 0;
    padding: 12px 16px 12px 16px;
  }

  .close:hover {
    background-color: #f44336;
    color: white;
  }

  /* Style the header */
  .header {
    background-color: #e07b08;
    padding: 30px 40px;
    color: white;
    text-align: center;
  }

  /* Clear floats after the header */
  .header:after {
    content: "";
    display: table;
    clear: both;
  }

  /* Style the input */
  input {
    margin: 0;
    border: none;
    border-radius: 0;
    width: 75%;
    padding: 10px;
    float: left;
    font-size: 16px;
  }

  /* Style the "Add" button */
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

<main>
  <div class="header">
    <h2 style="margin:5px">To Do List</h2>
    <input type="text" bind:value={todoText} placeholder="Title..." />
    <span on:click={addTodos} class="addBtn">Add</span>
  </div>
  <ul>
    {#each todos as todo, i}
      <li
        class:checked={todo.class !== false}
        on:click={changeClass(todos, todo)}>
        {todo.text}
        <span on:click={removeItemOnce(todos, todo)} class="close">x</span>
      </li>
    {/each}
  </ul>
</main>
