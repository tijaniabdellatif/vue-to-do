<template>
    <section class="todoapp">

        <header>
            <h1>
                Todos
            </h1>
            <input type="text" class="new-todo" placeholder="add task" v-model="newTodo" @keyup.enter="addTodo"/>
        </header>

        <div class="main">

            <input type="checkbox" class="toggle" v-model="allDone" style="transform: translateY(-42px);" />

            <ul class="todo-list">
                <li class="todo" :key="todo" v-for="todo in filteredTodos" :class="{completed: todo.completed}">
                    <div class="view">
                        <input type="checkbox" v-model="todo.completed" class="toggle" />
                        <label>
                            {{todo.name}}
                        </label>

                        <button class="destroy" @click.prevent="deleteTodo(todo)"></button>
                    </div>
                </li>
            </ul>
        </div>

        <footer class="footer" v-show="hasTodo">
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

            <button class="clear-completed" v-show="doneTodo" @click.prevent="deleteCompleted">Clear</button>
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
            filter:'all',
           
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
       },

       deleteTodo(todo){

           this.todos = this.todos.filter(item => item !== todo)
       },

       deleteCompleted(){
             this.todos = this.todos.filter(todo => !todo.completed)
       }
   },

 /* Computed Value */
   computed:{

       doneTodo(){
            
            return this.todos.filter(todo => todo.completed).length
       },

       hasTodo(){
          return this.todos.length > 0;

       },
      
      allDone:{

         get(){
            
            return this.remaining  === 0;
         },

         set(value){

                 this.todos.forEach(todo => {
                     todo.completed = value;
                 })
         }
      },

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
