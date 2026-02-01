<script setup lang="ts">
import router from '@/router';
import { getTodo, todoExists, type Todo } from '@/todos';

interface Props {
    todoId: number;
}

const props = defineProps<Props>();

if (!Number.isInteger(props.todoId)) {
    router.push("/");
}

if (!todoExists(props.todoId)) {
    router.push("/");
}

const todo: Todo = getTodo(props.todoId)!;

async function onConfirm() {
    await router.push("/");
}

</script>

<template>
    <main>
        <div>
            Here: {{ todo.description }}
        </div>
        <RouterLink to="/">
            Cancel
        </RouterLink>
        <br>
        <button @click="onConfirm" class="btn btn-link p-0">
            Confirm
        </button>
    </main>
</template>
