<template>
  <div id="app">
    <Container>
      <template v-slot:header>
        <h1>Vue Todo</h1>
      </template>
      <template v-slot:body>
        <TodoList></TodoList>
      </template>
      <template v-slot:footer>
        <p>Built by Mohamed Omar</p>
      </template>
    </Container>
  </div>
</template>

<script>
import Container from './components/Container'
import TodoList from './components/TodoList'
import './styles/normalize.css'

export default {
  name: 'App',
  components: {
    Container,
    TodoList,
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding: 0.4rem 1rem;
}
</style>
