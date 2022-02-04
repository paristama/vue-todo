<template>
  <ul class="divide-y divide-gray-400">
    <Todo
      v-for="(todo, index) in todos"
      :key="index"
      :todo="todo"
      :index="index"
      @removeTodo="removeTodo(index)"
    />
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
  emits: ["removeTodo"],
  props: {
    todos: Array,
    totalTodo: Number,
  },
  methods: {
    removeTodo(todoIndex) {
      this.$emit("removeTodo", todoIndex);
    },
  },
};
</script>
