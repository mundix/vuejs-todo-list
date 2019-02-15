<template>
    <div class="todo-item">
        <div class='todo-item-left'>
            <input type="checkbox" class="" v-model='todo.completed'>
            <div class="todo-item-lable" :class="{completed:todo.completed}" v-if="!todo.editing" @dblclick="editTodo(todo)" >{{todo.title}}</div>
            <input v-else  type="text" v-model='todo.title' class="todo-item-edit"  @blur="doneEdit(todo)" v-focus @keyup.esc="cancelEdit(todo)">
        </div>
        <div class="remove-item" @click="removeTodo(index)">
            &times;
        </div>
    </div>
</template>

<script>
    export default {
        name: "todo-item"
    }
</script>

<style scoped>

</style>