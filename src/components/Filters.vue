<script>
export default {
  name: "TodoFilter",
};
</script>

<template>
  <ul class="space-x-3 flex">
    <li>
      <button class="font-semibold text-gray-700" type="button">全部</button>
    </li>
    <li>
      <button class="font-semibold text-gray-300" type="button">未完成</button>
    </li>
    <li>
      <button class="font-semibold text-gray-300" type="button">已完成</button>
    </li>
  </ul>
</template>
