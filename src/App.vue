<template>
  <div id="app">
    <h1>List Kegiatan</h1>
    <div class="input-container">
      <input 
        v-model="newTodo" 
        @keyup.enter="addTodo" 
        placeholder="masukkan list" 
      />
      <button @click="addTodo">Tambahkan</button>
    </div>
    <ul>
      <li v-for="(todo, index) in todos" :key="index" class="todo-item">
        <input type="checkbox" v-model="todo.completed" />
        <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
        <button @click="deleteTodo(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'TodoList',
  setup() {
    const todos = ref([]);
    const newTodo = ref('');

    const addTodo = () => {
      if (newTodo.value.trim()) {
        todos.value.push({ text: newTodo.value.trim(), completed: false });
        newTodo.value = '';
      }
    };

    const deleteTodo = (index) => {
      todos.value.splice(index, 1);
    };

    return {
      todos,
      newTodo,
      addTodo,
      deleteTodo,
    };
  },
};
</script>

<style scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  background-color: #f4f4f4;
  text-align: center;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  max-width: 500px;
  margin: 50px auto;
  background-color: #fdf6e3; /* Light brown background */
}

h1 {
  color: #b33a3a; /* Dark red color */
  font-size: 2.5em;
  margin-bottom: 20px;
}

.input-container {
  margin-bottom: 20px;
  display: flex;
  justify-content: center;
}

input {
  margin-right: 10px;
  padding: 10px;
  font-size: 16px;
  border: 2px solid #a3a3a3; /* Grey border */
  border-radius: 5px;
  width: 60%;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
}

input:focus {
  border-color: #b33a3a; /* Dark red focus color */
  box-shadow: 0 2px 10px rgba(179, 58, 58, 0.3);
}

button {
  padding: 10px 15px;
  font-size: 16px;
  color: #fff;
  background-color: #b33a3a; /* Dark red button color */
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease, box-shadow 0.3s ease;
}

button:hover {
  background-color: #8c2b2b; /* Darker red on hover */
  box-shadow: 0 2px 10px rgba(140, 43, 43, 0.3);
}

ul {
  list-style-type: none;
  padding: 0;
}

li.todo-item {
  margin: 10px 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background-color: #fff;
  border: 2px solid #a3a3a3; /* Grey border */
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
}

li.todo-item:hover {
  border-color: #b33a3a; /* Dark red border on hover */
  box-shadow: 0 2px 10px rgba(179, 58, 58, 0.1);
}

li button {
  margin-left: 10px;
  padding: 5px 10px;
  font-size: 14px;
  color: #fff;
  background-color: #b33a3a; /* Dark red button color */
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease, box-shadow 0.3s ease;
}

li button:hover {
  background-color: #8c2b2b; /* Darker red on hover */
  box-shadow: 0 2px 10px rgba(140, 43, 43, 0.3);
}

.completed {
  text-decoration: line-through;
  color: #a3a3a3; /* Grey color for completed tasks */
}
</style>
