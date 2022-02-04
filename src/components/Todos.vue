<template>
  <ul class="divide-y divide-gray-400">
    <Todo v-for="todo in todos" :key="todo" :todo="todo" />
  </ul>
  <div class="mt-3">
    <p class="text-right text-sm text-gray-400">
      You have {{ totalTodo }} pending task
    </p>
  </div>
</template>

<script>
import Todo from "./Todo.vue";
export default {
  components: { Todo },
  props: {
    todos: Array,
    totalTodo: Number,
  },
};
</script>

<style></style>
