<template>
    <div class="relative h-full">
        <ul
            class="divide-y divide-gray-400 mb-8 max-h-full overflow-auto absolute w-full"
            ref="todoList"
        >
            <Todo
                v-for="(todo, index) in todos"
                :key="index"
                :todo="todo"
                :index="index"
                @showModal="showModal(index)"
                @toggleDone="toggleDone(index)"
            />
        </ul>
    </div>
    <div class="mt-4">
        <p class="text-right text-xs text-gray-400">
            You have {{ totalTodo }} pending task
        </p>
    </div>
</template>

<script>
import Todo from "./Todo.vue";
import { onMounted, ref } from "vue";
export default {
    components: { Todo },
    emits: ["showModal", "toggleDone", "update:modelValue"],
    props: {
        todos: Array,
        totalTodo: Number,
        modelValue: Object,
    },
    setup(props, { emit }) {
        // Untuk menggunakan this refs pada composition API perlu mendeklarasikan sebelum mounted
        // lalu mereturn refnya untuk dapat digunakan
        const todoList = ref(null);
        const showModal = (todoIndex) => {
            emit("showModal", todoIndex);
        };

        const toggleDone = (todoIndex) => {
            emit("toggleDone", todoIndex);
        };

        onMounted(() => {
            emit("update:modelValue", todoList.value.children);
        });

        return { showModal, toggleDone, todoList };
    },
};
</script>

<style></style>
