<template>
    <div class="app">
      <h1>Todo App</h1>
      <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Add a new todo...">
      <ul>
        <li v-for="(todo, index) in todos" :key="index" class="todo-item">
          <input type="checkbox" v-model="todo.completed" @change="deleteIfCompleted(index)">
          <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        newTodo: '',
        todos: []
      };
    },
    methods: {
      addTodo() {
        if (this.newTodo.trim()) {
          this.todos.push({ text: this.newTodo.trim(), completed: false });
          this.newTodo = '';
        }
      },
      deleteIfCompleted(index) {
        if (this.todos[index].completed) {
          this.todos.splice(index, 1);
        }
      }
    }
  }
  </script>
  

  <style>
/* Base styling for the entire app container */
.app {
  font-family: 'Roboto', sans-serif;
  max-width: 600px;
  margin: 5% auto;
  padding: 30px;
  border-radius: 12px;
  background-color: #fafafa;
  box-shadow: 0px 5px 20px rgba(0, 0, 0, 0.1);
}

/* Centered title with some typographical enhancements */
h1 {
  text-align: center;
  color: #333;
  font-weight: 400;
}

/* Styling for the input field with transition for a smoother effect */
input[type="text"] {
  width: 100%;
  padding: 12px 15px;
  margin-bottom: 30px;
  border-radius: 8px;
  border: 1px solid #ccc;
  transition: border-color 0.3s;
}

input[type="text"]:focus {
  border-color: #007BFF;
  outline: none;
}

/* Styling for the todo list */
ul {
  list-style-type: none;
  padding: 0;
}

/* Each todo item styling with hover effect and transition */
.todo-item {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
  padding: 10px;
  border-radius: 8px;
  background-color: #fff;
  transition: background-color 0.3s;
}

.todo-item:hover {
  background-color: #f7f7f7;
}

/* Styling for completed todos */
.todo-item span.completed {
  text-decoration: line-through;
  color: #aaa;
}

/* Checkbox styling and checked behavior */
input[type="checkbox"] {
  margin-right: 10px;
  cursor: pointer;
}

/* Add a slight scale effect for todo items on hover for an interactive feel */
.todo-item:hover {
  transform: scale(1.02);
}
</style>
