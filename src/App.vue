<template>
  <div
    class="bg-gray-800 px-4 py-10 shadow-lg my-6 w-full rounded-md md:max-w-lg text-white"
  >
    <h1
      class="text-4xl py-10 text-center font-extrabold bg-gradient-to-r from-blue-500 via-green-500 to-cyan-500 bg-clip-text text-transparent"
    >
      VUE TODO APP
    </h1>
    <form @submit.prevent="addTodo" class="mt-8 mb-8">
      <div class="flex space-x-2">
        <input
          type="text"
          class="bg-gray-600 flex-1 rounded-md px-4 py-2 text-sm focus:bg-white focus:text-black focus-visible:outline-green-500"
          placeholder="Type a new todo"
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
      @showModal="showModal"
      @toggleDone="toggleDone"
    />
  </div>
  <Modal
    :model-value="open"
    @update:model-value="open = $event"
    :todo="selectedTodo"
    @removeTodo="removeTodo"
  />
</template>

<script>
import Todos from "./components/Todos.vue";
import Modal from "./components/Modal.vue";
export default {
  components: { Todos, Modal },
  data() {
    return {
      selectedTodo: {},
      open: false,
      newTodo: "",
      todos: [],
    };
  },
  mounted() {
    this.todos = this.loadTodosLocalStorage();
  },
  computed: {
    totalTodo() {
      return this.todos.length;
    },
  },
  methods: {
    addTodo() {
      this.todos.push({ activity: this.newTodo, isDone: false });
      this.saveTodosLocalStorage();
      this.newTodo = "";
    },
    removeTodo(todoIndex) {
      this.todos.splice(todoIndex, 1);
      this.saveTodosLocalStorage();
    },
    toggleDone(todoIndex) {
      this.todos.forEach((todo, index) => {
        if (index === todoIndex) todo.isDone = !todo.isDone;
      });
      this.saveTodosLocalStorage();
    },
    loadTodosLocalStorage() {
      return JSON.parse(localStorage.getItem("todos")) ?? [];
    },
    saveTodosLocalStorage() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    showModal(data) {
      this.selectedTodo = { index: data, ...this.todos[data] };
      this.open = true;
    },
  },
};
</script>
