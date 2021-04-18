<template>
  <div>
    <h3>Go ahead, add one</h3>
    <form>
      <label for="todo-text">
        <input id="todo-text" v-model="text" type="text"
      /></label>
      <button :disabled="!text" @click.prevent="addTodo" type="submit">
        Submit
      </button>
      <div>
        <ul v-for="todo in todos" v-bind:key="todo.id">
          <li>
            <span v-bind:class="{ completed: todo.completed }">{{
              todo.text
            }}</span>
            <button @click.prevent="removeTodo(todo.id)">X</button>
            <button @click.prevent="completeTodo(todo.id)">Complete</button>
          </li>
        </ul>
      </div>
    </form>
  </div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid'

export default {
  data: function () {
    return {
      todos: [],
      text: '',
    }
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
.container {
  width: 100%;
}

.completed {
  text-decoration: line-through;
}
</style>
