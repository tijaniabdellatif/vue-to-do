<template>
    <section class="todoapp">

        <header>
            <h1>
                Todos
            </h1>
            <input type="text" class="new-todo" placeholder="add task" v-model="newTodo" @keyup.enter="addTodo"/>
        </header>

        <div class="main">
            <ul class="todo-list">
                <li class="todo" :key="todo" v-for="todo in todos" :class="{completed: todo.completed}">
                    <div class="view">
                        <input type="checkbox" v-model="todo.completed" class="toggle" />
                        <label>
                            {{todo.name}}
                        </label>
                    </div>
                </li>
            </ul>
        </div>
    </section>
</template>


<script>

export default {

  /* State with data() */
   data (){
        return {
            todos:[{
                name : 'Test Task',
                completed : false
            }],
            newTodo : ''
        } 
   },

   methods: {
       addTodo(){
           this.todos.push({
               completed : false,
               name:this.newTodo
           })
           this.newTodo = ''
       }
   },

}

</script>


<style src="./todos.css">

</style>
