<template>
  <div class="todo-list">
    <h3>Go ahead, add one</h3>
    <form>
      <label for="todo-text">
        <input id="todo-text" v-model="text" type="text"
      /></label>
      <button :disabled="!text" @click.prevent="addTodo" type="submit">
        Submit
      </button>
    </form>
    <ul v-for="todo in todos" v-bind:key="todo.id">
      <TodoItem
        v-bind:todoItem="todo"
        v-on:remove-todo="removeTodo($event)"
        v-on:complete-todo="completeTodo($event)"
      >
      </TodoItem>
    </ul>
  </div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid'
import TodoItem from './TodoItem'

export default {
  data: function () {
    return {
      todos: [],
      text: '',
    }
  },
  components: {
    TodoItem,
  },
  methods: {
    addTodo: function () {
      if (!this.text) {
        return
      }
      let newTodo = {
        text: this.text,
        id: uuidv4(),
        completed: false,
      }
      this.todos = [newTodo, ...this.todos]
      this.text = ''
    },
    removeTodo: function (id) {
      this.todos = this.todos.filter((todo) => {
        return todo.id !== id
      })
    },
    completeTodo: function (id) {
      let currentTodo = this.todos.find((todo) => todo.id === id)
      currentTodo.completed = true
    },
  },
}
</script>

<style scoped>
.todo-list {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
