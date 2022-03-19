<template>
    <li class="py-2 flex">
        <div class="ml-3 w-full flex justify-between items-center">
            <p
                :class="[
                    'text-sm flex-1 cursor-pointer',
                    { 'line-through text-gray-600': todo.isDone },
                ]"
                @click="toggleDone(index)"
            >
                {{ todo.activity }}
            </p>
            <button
                class="text-gray-500 p-1.5 cursor-pointer rounded-full hover:bg-red-300 hover:text-red-500"
                @click="showModal(index)"
            >
                <TrashIcon class="h-5 w-5" />
            </button>
        </div>
    </li>
</template>

<script>
import { TrashIcon } from "@heroicons/vue/outline";
export default {
    components: { TrashIcon },
    props: {
        todo: Object,
        index: Number,
    },
    setup(props, { emit }) {
        const showModal = (todoIndex) => {
            emit("showModal", todoIndex);
        };
        const toggleDone = (todoIndex) => {
            emit("toggleDone", todoIndex);
        };

        return { showModal, toggleDone };
    },
};
</script>

<style></style>
