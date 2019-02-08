<template>
    <div>
        <input type="text" class="todo-input" placeholder="What need to be done">
        Todo List goes here
    </div>
</template>

<script>
export default {
  name: 'todo-list',
  data () {
    return {
      
    }
  }
}
</script>

<style lang="scss">
    .todo-input {

        width: 100%;
        padding: 10px 18px;
        font-size: 18px;
        margin-bottom: 16px;

        a:focus{
            outline:0
        }
    }
</style>
