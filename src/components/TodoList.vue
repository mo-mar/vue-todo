<template>
  <div class="todo-list">
    <h2>Go ahead, add one</h2>
    <form>
      <label for="todo-text">
        <input id="todo-text" v-model="text" type="text"
      /></label>
      <button
        class="submit-button"
        :disabled="!text"
        @click.prevent="addTodo"
        type="submit"
      >
        Submit
      </button>
    </form>
    <ul>
      <TodoItem
        v-for="(todo, index) in todos"
        v-bind:key="todo.id"
        v-bind:todoItem="todo"
        v-bind:index="index"
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
      currentTodo.completed = !currentTodo.completed
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
  max-height: 600px;
}

ul {
  width: 50%;
  overflow-y: auto;
}

.todo-list form {
  margin-bottom: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.submit-button {
  height: 40px;
  padding: 0.8rem 1rem;
  vertical-align: middle;
  border-radius: 2px 8px 2px;
  height: 45px;
}

.todo-list form input {
  margin-bottom: 0.5rem;
  padding: 0.7rem;
  text-align: center;
}
</style>
