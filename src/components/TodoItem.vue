<template>
    <li>
      <span v-bind:class="{ donetask: todo.completed }">
        <input type="checkbox"
               @change="todo.completed = !todo.completed"
        >
        <strong>{{ index + 1 }}.</strong>
        {{ todo.title }}
      </span>
      <button class="todo-button"
              @click="$emit('remove-todo', todo.id)"
      >&times;</button>
    </li>
</template>

<script>
    export default {
        name: "TodoItem",
        props: {
          todo: {
            type: Object,
            required: true
          },
          index: Number,
        }
    }
</script>

<style scoped>
  li {
    border: 1px solid #ccc;
    display: flex;
    justify-content: space-between;
    padding: .5rem 2rem;
    margin-bottom: 0.5rem;
    align-items: center;
  }

  .todo-button {
    height: 12px;
    border: none;
    background-color: transparent;
    font-size: 24px;
    color: #acacac;
    outline: none;
    cursor: pointer;
    display: flex;
    align-items: center;
    font-weight: bold;
  }

  .todo-button:hover {
    color: #000;
  }

  input {
    margin-right: 1rem;
  }

  .donetask {
    text-decoration: line-through;
    color: #acacac;
  }
</style>
