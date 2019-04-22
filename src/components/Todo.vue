<template>
  <div class='ui centered card'>
    <div class="content" v-show="!isEditing">
      <div class='header'>
          {{ todo.title }}
      </div>
      <div class='meta'>
          {{ todo.project }}
      </div>
      <div class='extra content'>
        <input type="button" value="edit" v-on:click="showForm" >
        <input type="button" value="delete" @click="deleteTodo(todo)">
      </div>
    </div>
    
    <div class="content" v-show="isEditing">
      <div class='ui form'>
        <div class='field'>
          <label>Title</label>
          <input type='text' v-model="todo.title" >
        </div>
        <div class='field'>
          <label>Project</label>
          <input type='text' v-model="todo.project" >
        </div>
        <div class='ui two button attached buttons'>
          <button class='ui basic blue button' v-on:click="hideForm">
            Done
          </button>
        </div>
      </div>
    </div>
    <div class='ui bottom attached green basic button' @click="pendingTodo(todo)" v-show="!isEditing &&todo.done">
        Completed
    </div>
    <div class='ui bottom attached red basic button' @click="completeTodo(todo)" v-show="!isEditing && !todo.done">
        Pending
    </div>
  </div>
</template>



<script type="text/javascript">
  export default {
    props: ['todo'],
    data() {
      return {
        isEditing: false,
      };
    },
    methods: {  
      completeTodo(todo) {
        this.$emit('complete-todo',todo);
      },
      pendingTodo(todo){
        this.$emit('pending-todo',todo);
      },
      deleteTodo(todo) {
        this.$emit('delete-todo',todo);
      },
      showForm() {
        this.isEditing = true;
      },
      hideForm() {
        this.isEditing = false;
      },
    },
  };
</script>
