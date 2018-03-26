<template>
  <div class="todoList">
    <div class="title"> Welcome to Todo Application</div>
      <p>Completed Tasks: {{todos.filter(todo => {return todo.done === true}).length}}</p>
      <p>Pending Tasks: {{todos.filter(todo => {return todo.done === false}).length}}</p>
    <Todo v-for="(todo, index) in todos"
          v-bind:todo="todo" 
          v-bind:key="index" 
          v-on:delete-todo='deleteTodo(todo)'
          v-on:change-status='changeStatus(todo)'
    />
    <FormCreate v-on:create-todo='createTodo' />
  </div>
</template>

<script>
  import Todo from './Todo.vue';
  import FormCreate from './FormCreate.vue';
  import swal from 'sweetalert';
  export default {
    props: ['todos'],
    components: {
      Todo, FormCreate
    },
    methods: {
      deleteTodo(todo) {
        const todoIndex = this.todos.indexOf(todo);
        this.todos.splice(todoIndex, 1);
        swal({
          title: "Success",
          text: "You have deleted todo",
          icon: "success",
        });
      },

      createTodo(todo) {
        this.todos.push(todo);
        swal({
          title: "Success",
          text: "You have created todo",
          icon: "success",
        });
      },

      changeStatus(todo){
        const todoIndex = this.todos.indexOf(todo);
        this.todos[todoIndex].done = !this.todos[todoIndex].done;
        swal({
          title: "Success",
          text: "You have changed status",
          icon: "success",
        });
      }
    }
  }
</script>

<style scoped>
  h3 {
    margin: 40px 0 0;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }
</style>
