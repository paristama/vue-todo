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
export default {
    components: { Todo },
    emits: ["showModal", "toggleDone", "update:modelValue"],
    props: {
        todos: Array,
        totalTodo: Number,
        modelValue: Object,
    },
    methods: {
        showModal(todoIndex) {
            this.$emit("showModal", todoIndex);
        },
        toggleDone(todoIndex) {
            this.$emit("toggleDone", todoIndex);
        },
    },
    mounted() {
        this.$emit("update:modelValue", this.$refs.todoList.children);
    },
};
</script>
