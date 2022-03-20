<template>
    <div
        class="bg-gray-800 px-4 py-10 shadow-lg my-6 w-full rounded-md md:max-w-lg text-white max-h-full flex flex-col"
    >
        <h1
            class="text-4xl py-10 text-center font-extrabold bg-gradient-to-r from-blue-500 via-green-500 to-cyan-500 bg-clip-text text-transparent"
        >
            VUE TODO APP
        </h1>
        <form @submit.prevent="addTodo" class="mt-8 mb-8">
            <div
                class="flex flex-col space-y-2 sm:flex-row sm:space-x-2 sm:space-y-0"
            >
                <input
                    type="text"
                    class="bg-gray-700 flex-1 rounded-md px-4 py-2 text-sm focus:bg-gray-800 focus:placeholder:text-gray-600"
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
        <Search :todos="list" :todoList="todoList.list" />
        <Todos
            :todos="list"
            :totalTodo="totalTodo"
            @showModal="showModal"
            @toggleDone="toggleDone"
            v-model="todoList.list"
        />
    </div>
    <Modal
        :model-value="open"
        @update:model-value="open = $event"
        :todo="selectedTodo.item"
        @removeTodo="removeTodo"
    />
</template>

<script>
import Todos from "./Todos.vue";
import Modal from "./Modal.vue";
import Search from "./Search.vue";
import { ref, reactive, toRefs, computed, onMounted } from "vue";
export default {
    components: { Todos, Modal, Search },
    setup() {
        const open = ref(false);
        const newTodo = ref("");
        const todos = reactive({
            list: [],
        });
        const todoList = reactive({
            list: {},
        });
        const selectedTodo = reactive({
            item: {},
        });

        // Lifecycle
        onMounted(() => {
            todos.list = loadTodosLocalStorage();
        });

        const totalTodo = computed(() => {
            return todos.list.length;
        });

        // Methods
        const addTodo = () => {
            todos.list.push({
                activity: newTodo.value,
                isDone: false,
            });
            saveTodosLocalStorage();
            newTodo.value = "";
        };

        const removeTodo = (todoIndex) => {
            todos.list.splice(todoIndex, 1);
            saveTodosLocalStorage();
        };

        const toggleDone = (todoIndex) => {
            todos.list.forEach((todo, index) => {
                if (index === todoIndex) todo.isDone = !todo.isDone;
            });
            saveTodosLocalStorage();
        };

        const showModal = (data) => {
            selectedTodo.item = {
                index: data,
                ...todos.list[data],
            };
            open.value = true;
        };

        const loadTodosLocalStorage = () => {
            return JSON.parse(localStorage.getItem("todos")) ?? [];
        };
        const saveTodosLocalStorage = () => {
            localStorage.setItem("todos", JSON.stringify(todos.list));
        };

        return {
            open,
            newTodo,
            ...toRefs(todos),
            totalTodo,
            selectedTodo,
            todoList,
            addTodo,
            showModal,
            toggleDone,
            removeTodo,
        };
    },
};
</script>
<style></style>
