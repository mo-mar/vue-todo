<template>
  <li class="todo-item">
    <div v-bind:class="{ completed: todoItem.completed }">
      <div class="todo-information">
        <span>{{ index + 1 }}. </span
        ><span class="todo-text">{{ todoItem.text }}</span>
      </div>
    </div>
    <div class="todo-item__actions">
      <button @click.prevent="removeTodo(todoItem.id)">&#x2715;</button>
      <button
        v-if="!todoItem.completed"
        @click.prevent="completeTodo(todoItem.id)"
      >
        Complete
      </button>
      <button v-else @click.prevent="completeTodo(todoItem.id)">
        Uncomplete
      </button>
    </div>
  </li>
</template>

<script>
export default {
  props: ['todoItem', 'index'],
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
  margin-bottom: 0.5rem;
  background: white;
  border: 1px solid black;
  width: 100%;
}

.todo-information {
  font-size: 1.4rem;
}

.todo-text {
  width: 50%;
}

.todo-item__actions {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}

.todo-item__actions button {
  margin-bottom: 0.5rem;
}
.completed {
  text-decoration: line-through;
}
</style>
