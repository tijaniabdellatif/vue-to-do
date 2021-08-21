<template>
 
 <div>
   {{todos}}
   <todos v-model="todos"></todos>
  <todos v-model="todos"></todos>
      <todos v-model="todos"></todos>
     <button @click="addTodo">Add</button>
 </div>
</template>

<script>
import Todos from './components/Todos'

export default {
  data(){

    return {
      todos:[{
        name :'demo',
        completed:true
      }]
    }
  },
  name: 'App',
  components: {
    Todos
  },

  methods: {
    addTodo(){

      this.todos.push({

        name:'jean',
        completed:false
      })

    }
  },
}
</script>

<style>

</style>
