<template>
<li>
<span v-bind:class="{done: todo.completed}">
<input type="checkbox" v-on:change="todo.completed=!todo.completed">
<strong> {{index + 1}}</strong>
 {{todo.title}}
 <button class="rm" v-on:click="$emit('remove-todo', todo.id)">&times;</button>
 </span>
 </li>
</template>


<script>
export default{
props:{
   todo:{
   type: Object,
   required: true
   },
   index: Number
}
}
</script>


<style scoped>
li{
list-style-type: none;
display: flex;
justify-content: space-between;
}
.rm{
background: red;
}
.done{
text-decoration: line-through;
}
</style>
