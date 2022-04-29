<template>
  <div>
      <div v-bind:key="todo.id" v-for="todo in todos">
        <TodoList v-bind:todo = "todo"  v-on:del-todo="$emit('del-todo', todo.id)"/>
      </div>
  </div>

</template>

<script>
import TodoList from "./TodoList.vue";
export default {
    name:"TodoItem",
    components:{
      TodoList
    },
    props:["todos"]
    }
    
</script>

<style scope>

</style>