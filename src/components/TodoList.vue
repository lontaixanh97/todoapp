<template>
  <div>
    <p class="tasks">Completed Tasks: {{todos.filter(todo => {return todo.done === true}).length}}</p>
    <p class="tasks">Pending Tasks: {{todos.filter(todo => {return todo.done === false}).length}}</p>
    <div>
      <input type="radio" value="all" v-model="visibility" id="a">
      <input type="radio" value="completed" v-model="visibility" id="c">
      <input type="radio" value="pending" v-model="visibility" id="p">
    </div>
    <todo   @complete-todo="completeTodo" 
            @pending-todo="pendingTodo"  
            @delete-todo="deleteTodo"
            v-for="todo in filteredTodos" :todo.sync="todo" :key="todo.id" ></todo>
  </div>
</template>

<script type = "text/javascript" >
import Todo from './Todo';


export default {
  props: ['todos'],
  components: {
    Todo,
  },
  data: function(){ 
    return {
      visibility : '',
    }
  },
  computed: {
    filteredTodos: function () {
      return this.todos.filter(todo => {
        if (this.visibility === 'all')
          return todo;
        else if (this.visibility === 'completed')
          return todo.done == true;
        else
          return todo.done == false;
      })
    },
  },

  methods: {
    deleteTodo(todo){
        const todoIndex = this.todos.indexOf(todo);
        this.todos.splice(todoIndex, 1);
    },  
    completeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = true;
    },
    pendingTodo(todo){
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = false;
    }
  },
};
</script>

<style scoped>
p.tasks {
  text-align: center;
}
</style>

