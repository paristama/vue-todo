<template>
  <ul class="divide-y divide-gray-400 mb-8">
    <Todo
      v-for="(todo, index) in todos"
      :key="index"
      :todo="todo"
      :index="index"
      @removeTodo="removeTodo(index)"
      @toggleDone="toggleDone(index)"
    />
  </ul>
  <div>
    <p class="text-right text-xs text-gray-400">
      You have {{ totalTodo }} pending task
    </p>
  </div>
</template>

<script>
import Todo from "./Todo.vue";
export default {
  components: { Todo },
  emits: ["removeTodo", "toggleDone"],
  props: {
    todos: Array,
    totalTodo: Number,
  },
  methods: {
    removeTodo(todoIndex) {
      this.$emit("removeTodo", todoIndex);
    },
    toggleDone(todoIndex) {
      this.$emit("toggleDone", todoIndex);
    },
  },
};
</script>
