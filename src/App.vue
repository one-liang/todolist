<script>
import { computed, ref } from "vue";
import { useLocalStorage } from "@vueuse/core";

export default {
  setup() {
    const todos = useLocalStorage("todos", [
      {
        id: 1,
        content: "test",
        isDone: false,
      },
    ]);

    const addTodo = (newTodo) => {
      todos.value.push({
        id: Date.now(),
        content: newTodo,
        isDone: false,
      });
    };

    const updateState = (id, newState) => {
      const todoIndex = todos.value.findIndex((todo) => todo.id === id);
      if (todoIndex !== -1) {
        todos.value[todoIndex].isDone = newState;
      }
    };

    const updateTodo = (id, newContent) => {
      const todoIndex = todos.value.findIndex((todo) => todo.id === id);
      todos.value[todoIndex].content = newContent;
    };

    const deleteTodo = (id) => {
      const todoIndex = todos.value.findIndex((todo) => todo.id === id);
      todos.value.splice(todoIndex, 1);
    };

    const filter = ref("all");

    const filteredTodos = computed(() => {
      if (filter.value === "isDone") {
        return todos.value.filter((todo) => todo.isDone);
      } else if (filter.value === "unDone") {
        return todos.value.filter((todo) => !todo.isDone);
      }
      return todos.value;
    });

    const updatefilter = (newFilter) => {
      filter.value = newFilter;
    };

    return {
      todos,
      addTodo,
      updateState,
      updateTodo,
      deleteTodo,
      filter,
      filteredTodos,
      updatefilter,
    };
  },
};
</script>

<template>
  <div class="min-h-screen bg-gray-800 py-10">
    <h1 class="text-5xl text-white text-center font-semibold uppercase mb-8">Todolist</h1>
    <div class="max-w-md bg-gray-100 rounded-lg shadow-lg min-h-96 mx-auto p-8">
      <InputBox class="mb-6" @add-todo="addTodo" />

      <Filters :filter="filter" @update-filter="updatefilter" class="mb-4" />

      <transition-group
        tag="ul"
        class="space-y-4"
        enter-active-class="transition duration-300"
        enter-from-class="opacity-0 scale-90"
        enter-to-class="opacity-100 scale-100"
        leave-active-class="transition"
        leave-from-class="opacity-100 scale-100"
        leave-to-class="opacity-0 scale-90"
      >
        <List
          v-for="todo in filteredTodos"
          :key="todo.id"
          :todo="todo"
          @update-state="updateState"
          @update-todo="updateTodo"
          @delete-todo="deleteTodo"
        />
      </transition-group>
    </div>
  </div>
</template>
