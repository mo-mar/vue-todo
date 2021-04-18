<template>
  <li class="todo-item">
    <div v-bind:class="{ completed: todoItem.completed }">
      {{ todoItem.text }}
    </div>
    <div class="todo-item__actions">
      <button @click.prevent="removeTodo(todoItem.id)">X</button>
      <button @click.prevent="completeTodo(todoItem.id)">Complete</button>
    </div>
  </li>
</template>

<script>
export default {
  props: ['todoItem'],
  methods: {
    removeTodo: function (id) {
      this.$emit('remove-todo', id)
    },
    completeTodo: function (id) {
      this.$emit('complete-todo', id)
    },
  },
}
</script>

<style scoped>
.todo-item {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr;
  align-items: center;
  border: 1px solid lightblue;
  padding: 0.7rem;
  width: 100%;
  /* max-width: 500px; */
  margin-bottom: 0.5rem;
}

.todo-item__actions {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}
.completed {
  text-decoration: line-through;
}
</style>
