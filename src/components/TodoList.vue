<template>
    <div>
        <input type="text" class="todo-input" placeholder="What need to be done" v-model="newTodo" @keyup.enter="addTodo">
        <div v-for="todo in todos" :key="todo.id" class="todo-item">
            {{todo.title}}
        </div>
    </div>
</template>

<script>
export default {
  name: 'todo-list',
  data () {
    return {
      newTodo:'',
      idForTodo:3,
      todos: [
          {
              id:1,
              title:'May the force is with you',
              completed: false
          },
          {
              id:2,
              title: 'Bcause im batman',
              completed: false
          }
      ]
    }
  },
  methods:{
      addTodo(){
          this.todos.push({
              id:this.idForTodo,
              title:this.newTodo,
              completed:false
          });
            this.newTodo = '';
            this.idForTodo++; 
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
