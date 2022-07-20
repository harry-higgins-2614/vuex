<template>
  <div class="ui centered card">
    <!-- Todo shown when we are not in editing mode. -->
    <div class="content">
      <div class="header">{{ todo.title }}</div>
      <div class="meta">{{ todo.project }}</div>
      <div class="extra content">
        <span class="right floated trash icon" v-on:click="deleteItem(todo)">
          <i class="trash icon"></i>
        </span>
      </div>
    </div>
    <button
      class="ui bottom attached green basic button" v-show="todo.done" v-on:click="toggleDone()">
      Completed
    </button>
    <button
      class="ui bottom attached red basic button" v-show="!todo.done" v-on:click="toggleDone()">
      Pending
    </button>
  </div>
</template>

<script type="text/javascript">
import { mapState, mapActions } from 'vuex';
export default {
  props: {
    todo: {
      type: Object
    }
  },
  data() {
    return {
      newFormData: {}
    };
  },
  computed: {
    ...mapState({
      todos: state => state.todoList
    })
  },
  methods: {
    ...mapActions([
      'deleteTodo',
      'changeTodoTitle',
      'changeTodoProject',
      'toggleTodoDone'
    ]),
    deleteItem(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.deleteTodo(todoIndex);
    },
    changeTitle(event, todo) {

      const todoIndex = this.todos.indexOf(todo);
      var value = event.target.value;
      this.changeTodoTitle({ index: todoIndex, title: value });
    },
    changeProject(event, todo) {
      const todoIndex = this.todos.indexOf(todo);
      var value = event.target.value;
      this.changeTodoProject({ index: todoIndex, project: value });
    },
    toggleDone() { 
      const todoIndex = this.todos.indexOf(this.todo);
      this.toggleTodoDone({index: todoIndex});
    }
  }
};
</script>

<style lang="scss" scoped>
//Hacky just to remove the cursor on complete
.ui.bottom.attached.green.basic.button {
  cursor: default;
}
</style>
