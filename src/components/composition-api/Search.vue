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
import { ref, toRefs } from "vue";
export default {
    components: { SearchIcon },
    props: {
        todos: Array,
        todoList: Object,
    },
    setup(props) {
        const keyword = ref("");
        const { todos, todoList } = toRefs(props);

        const filterTodos = () => {
            todos.value.forEach((todo, index) => {
                if (
                    todo.activity
                        .toLowerCase()
                        .indexOf(keyword.value.toLowerCase()) !== -1
                ) {
                    todoList.value[index].style.display = "flex";
                } else todoList.value[index].style.display = "none";
            });
        };

        return { keyword, filterTodos };
    },
};
</script>
