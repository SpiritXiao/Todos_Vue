<template>
 <div class="todo-container">
    <div class="todo-wrap" >
     <TodoHeader :addItem='addItem'/>
     <TodoList :todos='todos' :deleteTodo='deleteTodo'/>
      <TodoFooter :todos='todos' :deleteCompletedTodos='deleteCompletedTodos' :selectAllTodos='selectAllTodos'/>
    </div>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader'
import TodoList from './components/TodoList'
import TodoFooter from './components/TodoFooter'

export default {
  data() {
    return {
      // todos:[
      //   {title:'eat',complete:false},
      //   {title:'read',complete:true},
      //   {title:'sleep',complete:false}
      // ]

      todos:JSON.parse(window.localStorage.getItem('todos_key') || '[]')
    }
  },
  methods: {
    addItem(todo){
      this.todos.unshift(todo)
    },
    deleteTodo(index){
      this.todos.splice(index,1)
    },
    deleteCompletedTodos(){
      this.todos=this.todos.filter(todo=> !todo.complete)
    },
    selectAllTodos(isCheck){
      this.todos.forEach(todo=>todo.complete=isCheck)
    }
  },
  watch:{
    todos:{
      deep:true,
      handler:function(newValue){
        window.localStorage.setItem('todos_key',JSON.stringify(newValue))
      }
    }
  },
  components: {
    TodoHeader,
    TodoList,
    TodoFooter
  }
}
</script>

<style>
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

</style>
