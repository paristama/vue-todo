<template>
  <ul class="divide-y divide-gray-400 mb-8">
    <Todo
      v-for="(todo, index) in todos"
      :key="index"
      :todo="todo"
      :index="index"
      @showModal="showModal(index)"
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
  emits: ["showModal", "toggleDone"],
  props: {
    todos: Array,
    totalTodo: Number,
  },
  methods: {
    showModal(todoIndex) {
      this.$emit("showModal", todoIndex);
    },
    toggleDone(todoIndex) {
      this.$emit("toggleDone", todoIndex);
    },
  },
};
</script>
