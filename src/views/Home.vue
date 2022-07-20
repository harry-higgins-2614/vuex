<template>
  <div id="app">
    <todo-list />
    <create-todo v-on:create-todo="createTodo"></create-todo>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList';
import CreateTodo from '@/components/CreateTodo';
import { mapActions, mapState } from 'vuex';

export default {
  name: 'home',
  components: {
    TodoList,
    CreateTodo
  },
  computed: {
    ...mapState({
      todos: state => state.todoList
    })
  },
  methods:
  {
    ...mapActions([
      'addToDo'
    ]),
    createTodo(newTodo) {
      this.addToDo(newTodo);
    }
  }

};
</script>
