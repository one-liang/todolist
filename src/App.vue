<script>
export default {};
</script>

<template>
  <div class="min-h-screen bg-gray-800 py-10">
    <h1 class="text-5xl text-white text-center font-semibold uppercase mb-8">Todolist</h1>
    <div class="max-w-md bg-gray-100 rounded-lg shadow-lg h-96 mx-auto p-8">
      <InputBox class="mb-6" />

      <Filters class="mb-4" />

      <ul class="space-y-4">
        <List v-for="item in 3" :key="item" />
      </ul>
    </div>
  </div>
</template>
