<template>
  <h1>Vue 3 Todo App</h1>
  <form @submit.prevent="addNewTodo">
    <label>New Todo</label>
    <input v-model="newTodo" />
    <button>Add New Todo</button>
  </form>
  <h2>{{ newTodo }}</h2>
  <ul>
    <li v-for="(todo, index) in todos" :key="todo.id" class="cursor">
      <h3 :class="{ underLine: todo.done }" @click="toggleDone(todo)">
        {{ todo.content }}
      </h3>
      <button @click="removeTodo(index)">Remove Todo</button>
    </li>
  </ul>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const newTodo = ref("");
    const todos = ref([]);

    function addNewTodo() {
      console.log(newTodo.value);
      todos.value.push({
        id: 1,
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }
    function toggleDone(todo) {
      todo.done = !todo.done;
    }
    function removeTodo(index) {
      todos.value.splice(index, 1);
    }
    return {
      toggleDone,
      todos,
      newTodo,
      addNewTodo,
      removeTodo,
    };
  },
};
</script>

<style>
body {
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 2em;
  width: 80%;
  margin: 0 auto;
}
.cursor {
  cursor: pointer;
}
.underLine {
  text-decoration: line-through;
}
</style>
