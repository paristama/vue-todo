<template>
  <div
    class="bg-gray-800 px-4 py-2 shadow-lg my-6 w-full rounded-md md:w-1/2 text-white"
  >
    <h1
      class="text-4xl text-center font-extrabold bg-gradient-to-r from-blue-500 via-green-500 to-cyan-500 bg-clip-text text-transparent"
    >
      VUE TODO APP
    </h1>
    <form @submit.prevent="addTodo" class="mt-8 mb-6">
      <div class="flex space-x-2">
        <input
          type="text"
          class="bg-gray-600 flex-1 rounded-md px-4 py-2 text-sm"
          placeholder="Type your todo"
          v-model="newTodo"
          autofocus
        />
        <button
          type="submit"
          class="bg-green-700 px-4 py-1.5 rounded-md text-sm"
        >
          Add Todo
        </button>
      </div>
    </form>
    <!-- <div class="w-full border border-white mb-6"></div> -->
    <Todos
      :todos="todos"
      :totalTodo="totalTodo"
      @removeTodo="removeTodo"
      @toggleDone="toggleDone"
    />
  </div>
</template>

<script>
import Todos from "./components/Todos.vue";
export default {
  components: { Todos },
  data() {
    return {
      newTodo: "",
      todos: [],
    };
  },
  computed: {
    totalTodo() {
      return this.todos.length;
    },
  },
  methods: {
    addTodo() {
      this.todos.push({ activity: this.newTodo, isDone: false });
      this.newTodo = "";
    },
    removeTodo(todoIndex) {
      this.todos.splice(todoIndex, 1);
    },
    toggleDone(todoIndex) {
      this.todos.forEach((todo, index) => {
        if (index === todoIndex) todo.isDone = !todo.isDone;
      });
    },
  },
};
</script>
