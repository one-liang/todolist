<script>
import { ref } from "vue";

export default {
  name: "List",
  emits: ["update-state"],
  props: {
    todo: {
      type: Object,
      default: () => {},
    },
  },
  setup(props, { emit }) {
    const newContent = ref(props.content);

    const updateState = (evt) => {
      emit("update-state", props.todo.id, evt.target.checked);
    };

    return {
      newContent,
      updateState
    };
  },
};
</script>

<template>
  <li class="flex justify-between px-4 py-2 bg-white rounded-md">
    <div class="flex items-center w-full space-x-3">
      <input
        class="w-5 h-5 text-gray-800 rounded-full cursor-pointer focus:ring-0 active:scale-90"
        type="checkbox"
        :checked="todo.isDone"
        @change="updateState"
      />
      <div
        class="w-full border-none px-2 text-gray-800 focus:ring-0 focus:border"
        :class="todo.isDone ? 'line-through' : ''"
      >{{ todo.content }}</div>
      <input
        v-model="newContent"
        class="w-full border-none px-2 text-gray-800 focus:ring-gray-800"
        type="text"
      />
    </div>
    <button class="text-gray-300 ml-3 hover:text-red-500 active:scale-90" type="button">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-4 w-4 fill-current"
        viewBox="0 0 20 20"
        fill="currentColor"
      >
        <path
          fill-rule="evenodd"
          d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z"
          clip-rule="evenodd"
        />
      </svg>
    </button>
  </li>
</template>
