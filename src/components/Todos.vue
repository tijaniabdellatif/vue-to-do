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
                <li class="todo" :key="todo" v-for="todo in filteredTodos" :class="{completed: todo.completed}">
                    <div class="view">
                        <input type="checkbox" v-model="todo.completed" class="toggle" />
                        <label>
                            {{todo.name}}
                        </label>
                    </div>
                </li>
            </ul>
        </div>

        <footer class="footer">
            <span class="todo-count">
               <strong>{{ remaining }}</strong> Tasks to do
            </span>

            <!--Systeme de filter-->
            <ul class="filters">
                <li>
                    <a href="#" :class="{selected : filter === 'all'}" @click.prevent="filter = 'all'">All tasks</a>
                </li>
                <li>
                    <a href="#" :class="{selected : filter === 'todo'}" @click.prevent="filter = 'todo'">Task to do</a>
                </li>
                <li>
                    <a href="#" :class="{selected : filter === 'done'}" @click.prevent="filter = 'done'">Tasks done</a>
                </li>
            </ul>
        </footer>
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
            newTodo : '',
            filter:'all'
        } 
   },

/* Methods */
   methods: {
       addTodo(){
           this.todos.push({
               completed : false,
               name:this.newTodo
           })
           this.newTodo = ''
       }
   },

 /* Computed Value */
   computed:{

       remaining(){
           return this.todos.filter(todo => !todo.completed).length
       },

       filteredTodos(){

          if(this.filter === 'todo')
          {
              return this.todos.filter(todo => !todo.completed)
          }
           
           else if(this.filter === 'done'){
                 return this.todos.filter(todo => todo.completed)
           }

           return this.todos
       }
   }

}

</script>


<style src="./todos.css">

</style>
