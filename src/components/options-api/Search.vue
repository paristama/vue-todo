<template>
  <div class="relative text-gray-500 mb-6 w-1/2 ml-auto">
    <input
      type="text"
      class="w-full right bg-transparent border-gray-600 border px-4 py-2 rounded-md text-sm focus:outline-none placeholder:text-gray-600"
      placeholder="Search todo..."
      v-model="keyword"
      @input="filterTodos"
    />
    <div class="absolute inset-y-0 flex items-center right-0 pr-1.5">
      <SearchIcon class="h-5 w-5" />
    </div>
  </div>
</template>

<script>
import { SearchIcon } from "@heroicons/vue/outline";
export default {
  components: { SearchIcon },
  props: {
    todos: Array,
    todoList: Object,
  },
  // emits: ["update:modelValue"],
  data() {
    return {
      keyword: "",
    };
  },
  methods: {
    filterTodos() {
      this.todos.forEach((todo, index) => {
        if (
          todo.activity.toLowerCase().indexOf(this.keyword.toLowerCase()) !== -1
        ) {
          this.todoList[index].style.display = "flex";
        } else this.todoList[index].style.display = "none";
      });
    },
  },
};
</script>
