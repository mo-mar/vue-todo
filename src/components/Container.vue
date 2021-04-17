<template>
  <div class="container">
    <header>
      <slot name="header"></slot>
    </header>
    <slot name="body"> </slot>
    <footer>
      <slot name="footer"></slot>
    </footer>
  </div>
</template>

<script>
export default {}
</script>

<style scoped>
.container {
  width: 100%;
  max-width: 1280px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: auto 1fr auto;
  height: 100vh;
}
</style>
