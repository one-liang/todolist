
<script>
import { ref } from "vue";
import { PlusIcon } from "@heroicons/vue/solid";

export default {
  name: "InputBox",
  components: {
    PlusIcon,
  },
  emits: ["add-todo"],
  setup(props, { emit }) {
    const newTodo = ref("");

    const handleAddTodo = () => {
      if (!newTodo.value) return;
      emit("add-todo", newTodo.value);

      newTodo.value = "";
    };

    return {
      newTodo,
      handleAddTodo,
    };
  },
};
</script>

<template>
  <form class="relative">
    <input
      v-model.trim="newTodo"
      class="w-full border-0 bg-white rounded-full duration-200 shadow-md pl-4 pr-12 focus:ring-0 focus:shadow-none"
      type="text"
    />
    <button
      class="absolute right-0 top-0 w-10 h-10 rounded-full bg-gray-800 text-white text-xl duration-200 hover:rotate-90 active:scale-90"
      type="button"
      @click="handleAddTodo"
    >
      <PlusIcon class="w-5 h-5 fill-current mx-auto" />
    </button>
  </form>
</template>
