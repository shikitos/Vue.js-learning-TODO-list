<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="title">
    <button type="submit">Create</button>
  </form>
</template>

<script>
    export default {
      name: "AddTodo",
      methods: {
        onSubmit() {
          if (this.title.trim()) {
            const newTodo = {
              id: Date.now(),
              title: this.title,
              completed: false,
            };

            this.$emit('add-todo', newTodo);
            this.title = '';
          }
        },
      },
      data() {
        return {
          title: '',
        }
      },
    }
</script>

<style scoped>
  form {
    display: flex;
    justify-content: center;
    height: 1.85rem;
  }
  input {
    width: 85%;
    border: 1px solid #ccc;
    border-right: none;
    outline: none;
  }
  button {
    outline: none;
    border: 1px solid #ccc;
    background-color: transparent;
    width: 15%;
    cursor: pointer;
  }
</style>
