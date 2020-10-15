<template>
   <div>
<h2>Todo</h2>

<AddTodo
@add-todo="addTodo"
/>

<select v-model="filter">
<option value="all">All</option>
<option value="completed">Completed</option>
<option value="not-completed">Not Completed</option>
</select>
<hr>
<TodoList
v-bind:todos="filteredTodos"

v-on:remove-todo="removeTodo"
/>

</div>
</template>


<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
export default {
  name: 'App',
  data(){
  return {
     todos: [],
     filter: 'all'
  }
  },
  mounted(){
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
  .then(response => response.json())
  .then(json => {
    this.todos = json
  })
  },
  computed:{
    filteredTodos(){
      if(this.filter === 'all'){
        return this.todos
      }
      if(this.filter === 'completed'){
        return this.todos.filter(t => t.completed)
      }
      if(this.filter === 'not-completed'){
        return this.todos.filter(t => !t.completed)
      }
    }
  },
  //watch: {
  //  filter(value){
  //    console.log(value)
  //  }
  //},
  methods: {
    removeTodo(id){
      console.log(id);
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  },
  components: {
     TodoList, AddTodo
  }
}
</script>
