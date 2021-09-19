<script>
export default {
  name: "TodoFilter",
  emits: ["update-filter"],
  props: {
    filter: {
      type: String,
      default: "all",
    },
  },
  setup(props, { emit }) {
    const updateFilter = (newFilter) => {
      emit("update-filter", newFilter);
    };

    return {
      updateFilter,
    };
  },
};
</script>

<template>
  <ul class="space-x-3 flex">
    <li>
      <button
        :class="filter === 'all' ? 'text-gray-700' : 'text-gray-300'"
        @click="updateFilter('all')"
        class="font-semibold"
        type="button"
      >全部</button>
    </li>
    <li>
      <button
        :class="filter === 'unDone' ? 'text-gray-700' : 'text-gray-300'"
        @click="updateFilter('unDone')"
        class="font-semibold"
        type="button"
      >未完成</button>
    </li>
    <li>
      <button
        :class="filter === 'isDone' ? 'text-gray-700' : 'text-gray-300'"
        @click="updateFilter('isDone')"
        class="font-semibold text-gray-300"
        type="button"
      >已完成</button>
    </li>
  </ul>
</template>
