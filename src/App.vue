<script>
import { ref } from "vue";

export default {
  setup() {
    const todos = ref([
      {
        id: 1,
        content: "test",
        isDone: false,
      },
    ]);

    const addTodo = (newTodo) => {
      console.log("addTodo", newTodo);
      todos.value.push({
        id: Date.now(),
        content: newTodo,
        isDone: false,
      });
    };

    const updateState = (id, newState) => {
      console.log("updateState", id, newState);
      const todoIndex = todos.value.findIndex(todo => todo.id === id);
      if (todoIndex !== -1) {
        todos.value[todoIndex].isDone = newState;
      }
    };

    return {
      todos,
      addTodo,
      updateState,
    };
  },
};
</script>

<template>
  <div class="min-h-screen bg-gray-800 py-10">
    <h1 class="text-5xl text-white text-center font-semibold uppercase mb-8">Todolist</h1>
    <div class="max-w-md bg-gray-100 rounded-lg shadow-lg h-96 mx-auto p-8">
      <InputBox class="mb-6" @add-todo="addTodo" />

      <Filters class="mb-4" />

      <ul class="space-y-4">
        <List v-for="todo in todos" :key="todo.id" :todo="todo" @update-state="updateState" />
      </ul>
    </div>
  </div>
</template>
