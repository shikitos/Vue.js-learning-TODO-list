<template>
  <div id='app'>
    <h1>Todo application</h1>
    <AddTodo
      @add-todo='addTodo'
    />
    <label>
      <select v-model='filter'>
        <option value='all' class=''>All</option>
        <option value='completed' class=''>Completed</option>
        <option value='not-completed' class=''>Not completed</option>
      </select>
    </label>
    <hr>
    <TodoList
      v-if='filteredTodos.length'
      v-bind:todos='filteredTodos'
      @remove-todo='removeTodo'
      />
    <p v-else>No todos...</p>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue';
import AddTodo from './components/AddTodo.vue';

export default {
  name: 'App',
  data() {
    return {
      todos: [
        {
          id: 1, title: 'Купить молоко', completed: false,
        },
        {
          id: 2, title: 'Купить хлеб', completed: false,
        },
        {
          id: 3, title: 'Купить pivo', completed: false,
        },
      ],
      filter: 'all',
    };
  },
  components: {
    TodoList, AddTodo,
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter((t) => t.id !== id);
    },
    addTodo(todo) {
      this.todos.push(todo);
      localStorage.setItem('todos', todo);
    },
  },
  computed: {
    filteredTodos() {
      if (this.filter === 'all') {
        return this.todos;
      }
      if (this.filter === 'completed') {
        return this.todos.filter((t) => t.completed);
      }
      if (this.filter === 'not-completed') {
        return this.todos.filter((t) => !t.completed);
      }
      return true;
    },
  },
};
</script>

<style lang='scss'>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
