<template>
  <div id="app">
    <h1 class="ui dividing centered header">Vue.js 2 - Приложение список задач</h1>
    <div class='ui three column centered grid'>
      <div class="column">
        <todo-list :todos="todos"></todo-list>
        <create-todo @create-todo="createTodo"></create-todo>
      </div>
    </div>
  </div>
</template>

<script>
import sweetalert from 'sweetalert';
import TodoList from './components/TodoList.vue';
import CreateTodo from './components/CreateTodo.vue';

export default {
  name: 'app',
  components: {
    TodoList,
    CreateTodo
  },
  data () {
    return {
      todos: [
        {
          title: 'Задача A',
          project: 'Проект A',
          done: false,
        },{
          title: 'Задача B',
          project: 'Проект B',
          done: true,
        },{
          title: 'Задача C',
          project: 'Проект C',
          done: false,
        },{
          title: 'Задача D',
          project: 'Проект D',
          done: false,
        }
      ]
    }
  },
  methods: {
    createTodo(newTodo) {
      this.todos.push(newTodo);
      sweetalert('Успех!', 'Задача создана!', 'success');
    }
  }
}
</script>

<style scoped>
  h1.dividing.header {
    padding: 20px 0;
  }
</style>
