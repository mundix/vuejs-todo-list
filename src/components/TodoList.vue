<template>
    <div>
        <input type="text" class="todo-input" placeholder="What need to be done" v-model="newTodo" @keyup.enter="addTodo">
        <!--<div v-for="(todo,index) in todos" :key="todo.id" class="todo-item">-->
        <!--Another computed property todosFiltered-->
        <!--We add the :todo="todo" :index="index" props-->
        <!--And for call back from the child component using $emit need to call a event here to call the method -->
        <todo-item v-for="(todo,index) in todosFiltered" :key="todo.id" :todo="todo" :index="index" @removedTodo="removeTodo">
            <!--<div class='todo-item-left'>-->
                <!--<input type="checkbox" class="" v-model='todo.completed'>-->
                <!--<div class="todo-item-lable" :class="{completed:todo.completed}" v-if="!todo.editing" @dblclick="editTodo(todo)" >{{todo.title}}</div>-->
                <!--<input v-else  type="text" v-model='todo.title' class="todo-item-edit"  @blur="doneEdit(todo)" v-focus @keyup.esc="cancelEdit(todo)">-->
            <!--</div>-->
            <!--<div class="remove-item" @click="removeTodo(index)">-->
                <!--&times;-->
            <!--</div>-->
        </todo-item><!--.todo-item-->
        <div class="extra-container">
          <div><label ><input type="checkbox" :checked="!anyRemaning" @change="checkAllTodos"> Check All</label></div>
          <div>{{remaining}} items left</div>
        </div>

        <div class="extra-container">
          <div>
              <button :class="{ active: filter === 'all' }" @click="filter = 'all'">All</button>
              <button :class="{ active: filter === 'active' }" @click="filter = 'active'">Active</button>
              <button :class="{ active: filter === 'completed' }" @click="filter = 'completed'">Completed</button>
          </div>
            <transition name="fade">
                <div>
                    <button v-if="showClearCompletedButton" @click="clearCompleted">Clear Completed</button>

                </div>
            </transition>
        </div>
    </div>
</template>

<script>

import TodoItem from '../components/TodoItem';

export default {
    name: 'todo-list',
    components:{
        TodoItem
    },
    data () {
    return {
      newTodo:'',
      idForTodo:6,
      beforeEditCache:'',
      // remaining:0,
      filter: 'all',
      todos: [
          {
              id:1,
              title:'Avengers: Infinity War',
              completed: false,
              editing:false,
          },
          {
              id:2,
              title: 'Avengers: Ends Game',
              completed: false,
              editing:false,
          },
          {
              id:3,
              title: 'The Matrix',
              completed: false,
              editing:false,
          },{
              id:4,
              title: 'The Incredibles',
              completed: false,
              editing:false,
          },{
              id:5,
              title: 'The Lord Of the Rings',
              completed: false,
              editing:false,
          }
      ]
    }
    },
    directives:{
    focus: {
      inserted: function(el) {
        el.focus();
      }
    }
    },
    computed:{
    remaining(){
      return this.todos.filter(todo => !todo.completed).length;
    },
    anyRemaning(){
      return this.remaining != 0;
    },
    todosFiltered(){
        if(this.filter === ' all') {
            return this.todos;
        }else if (this.filter === 'active'){
            return this.todos.filter(todo => !todo.completed);
        } else if(this.filter === 'completed'){
            return this.todos.filter(todo => todo.completed);
        }
        return this.todos;
    },
    showClearCompletedButton()
    {
        return this.todos.filter(todo => todo.completed).length > 0
    }
    },
    methods:{
      addTodo(){
          if (this.newTodo.trim().length === 0) {
              return;
          }

          this.todos.push({
              id:this.idForTodo,
              title:this.newTodo,
              completed:false
          });
            this.newTodo = '';
            this.idForTodo++;
      },
        // This called fromt he event @removedTodo by passing the method removeTodo and on the event $emit we passed the index
      removeTodo(index){
          console.log("Called Method from child ");
          this.todos.splice(index,1);
      },
      editTodo(todo) {
        this.beforeEditCache = todo.title;
        todo.editing = true;
      },
      doneEdit(todo){

        if (todo.title.trim() ===0) {
              todo.title = this.beforeEditCache;
              return;
          }

          todo.editing = false;
      },
      cancelEdit(todo){
        todo.title = this.beforeEditCache;
        todo.editing = false;
      },
      checkAllTodos()
      {
        this.todos.forEach((todo) =>  todo.completed = event.target.checked);
      },
      clearCompleted(){
          this.todos = this.todos.filter(todo => !todo.completed);
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
    .todo-item {
        margin-bottom: 12px;
        display: flex;
        align-items: center;
        justify-content:space-between;
    }

    .remove-item {
        cursor: pointer;
        margin-left: 14px;
        a:hover {
            color:black;
        }
    }


    .todo-item-left{
      display: flex;
      align-items:center;
    }

    .todo-item-label {
      padding: 10px;
      border: 1px solid white;
      margin-left: 12px;
    }

    .todo-item-edit {
      font-size:24px;
      color:#2c3e50;
      margin-left: 12px;
      width: 100%;
      padding: 10px;
      border:1px solid #ccc;
      font-family: 'Avenir',Arial, Helvetica, sans-serif;

      a:focus{
              outline:0;
          }
    }

    .completed {
      text-decoration:line-through;
      color:grey;
    }

    .extra-container {
      display: flex;
      align-items: center;
      justify-content: space-between;
      font-size: 16px;
      border-top: 1px solid lightgray;
      border-top: 14px;
      margin-bottom: 14px;
    }

    button {
      font-size:14px;
      background-color:white;
      appearance: none;

      a:hover {
        background: lightgray;
      }

      a:focus {
        outline: none;
      }
    }

    .active {
      background: lightgreen;
    }

    .fade-enter-active,.fade-leave-ative {
        transition: opacity .2s;
    }
    .fade-enter,.fade-leave-to{
        opacity: 0;
    }

</style>
