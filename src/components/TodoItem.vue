<template>
    <li>
        <span :class="{done: todo.completed}">
            <input type="checkbox" @change="todo.completed = !todo.completed">
            <strong>{{ index + 1 }}</strong>
            {{ todo.title }}
        </span>
        <button class="delete" @click="$emit('remove-todo', todo.id)">&times;</button>
        
    </li>
</template>

<script>
export default {
    props: {
        todo: {
            type: Object,
            required: true
        },
        index: Number
    }
}
</script>

<style scoped>
    li {
        border: 1px solid #ccc;
        display: flex;
        justify-content: space-between;
        padding: 5px 20px;
        margin-bottom: 10px;
    }
    .delete {
        background: red;
        color: #fff;
        border-radius: 50%;
        font-weight: bold;
    }
    .done {
        text-decoration: line-through;
        color:rgb(209, 201, 193);
    }
</style>