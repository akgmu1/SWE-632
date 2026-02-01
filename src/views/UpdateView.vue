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

async function onUpdate() {
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
        <button @click="onUpdate" class="btn btn-link p-0">
            Update
        </button>
        <br>
        <RouterLink :to="`/delete/${props.todoId}`">
            Delete
        </RouterLink>
    </main>
</template>
