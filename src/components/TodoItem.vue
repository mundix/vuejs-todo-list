<template>
    <div class="todo-item">
        <div class='todo-item-left'>
            <!--Since we have the data properties we don't need the todo.completed , only completed -->
            <!--<input type="checkbox" class="" v-model='todo.completed'>-->
            <input type="checkbox" class="" v-model='completed'>
            <div class="todo-item-lable" :class="{completed:completed}" v-if="!editing" @dblclick="" >{{title}}</div>
            <input v-else  type="text" v-model='title' class="todo-item-edit"  @blur="" v-focus @keyup.esc="cancelEdit">
        </div>
        <!--<div class="remove-item" @click="removeTodo(index)">-->
        <!--how we don't have the method in this componente we need to recreated on the componentent-->
        <div class="remove-item" @click="removeTodo(index)">
            &times;
        </div>
    </div>
</template>

<script>
    //in vue you can't mutate props
    export default {
        name: "todo-item",
        props:{
            //we define the type and the is required
            todo: {
                type: Object,
                required:true, //if we forget passed in
            },
            index: {
                type:Number,
                required: true
            }
        },
        data(){
            //For edit the mutations we need to create this variables to assign from the props de values.
            return  {
                'id':this.todo.id,
                'title': this.todo.title,
                'completed':this.todo.completed,
                'editing':this.todo.editing,
                'beforeEditCache' : ''
            }
        },
        methods:{
            //we can call from the child to the parent component
            removeTodo(index){
                this.$emit('removedTodo',index);
            }
        }

    }
</script>

<style scoped>

</style>