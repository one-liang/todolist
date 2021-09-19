<script>
import { ref, nextTick } from "vue";
import { TrashIcon } from "@heroicons/vue/solid";

export default {
  name: "List",
  components: {
    TrashIcon,
  },
  emits: ["update-state", "update-todo", "delete-todo"],
  props: {
    todo: {
      type: Object,
      default: () => {},
    },
  },
  setup(props, { emit }) {
    const isEditing = ref(false);

    const newContent = ref(props.todo.content);

    const editInput = ref(null);

    const isCancel = ref(false);

    const updateState = (evt) => {
      emit("update-state", props.todo.id, evt.target.checked);
    };

    const editTodo = () => {
      isEditing.value = true;

      nextTick(() => {
        editInput.value.focus();
      });
    };

    const updateTodo = () => {
      if (!isEditing.value) return;

      if (isCancel.value) {
        isCancel.value = false;
        return;
      }

      emit("update-todo", props.todo.id, newContent.value);
      isEditing.value = false;
    };

    const cancelEdit = () => {
      isCancel.value = true;
      newContent.value = props.todo.content;
      isEditing.value = false;
    };

    const deleteTodo = () => {
      emit("delete-todo", props.todo.id);
    };

    return {
      isEditing,
      newContent,
      editInput,
      isCancel,
      updateState,
      editTodo,
      updateTodo,
      cancelEdit,
      deleteTodo,
    };
  },
};
</script>

<template>
  <li class="flex justify-between px-4 py-3 bg-white rounded-md">
    <div class="flex items-center w-full h-10 space-x-3">
      <input
        class="w-5 h-5 text-gray-800 rounded-full cursor-pointer focus:ring-0 active:scale-90"
        type="checkbox"
        :checked="todo.isDone"
        @change="updateState"
      />
      <div
        v-if="!isEditing"
        class="w-full h-10 leading-10 border-none px-2 text-gray-800 focus:ring-0 focus:border"
        :class="todo.isDone ? 'line-through' : ''"
        @dblclick="editTodo"
      >{{ todo.content }}</div>
      <input
        ref="editInput"
        v-if="isEditing"
        v-model.trim="newContent"
        class="w-full border-none px-2 rounded-md text-gray-800 focus:ring-gray-800"
        type="text"
        @blur="updateTodo"
        @keydown.enter="updateTodo"
        @keydown.esc="cancelEdit"
      />
    </div>
    <button
      class="text-gray-300 ml-3 hover:text-red-500 active:scale-90"
      type="button"
      @click="deleteTodo"
    >
      <TrashIcon class="h-4 w-4 fill-current" />
    </button>
  </li>
</template>
