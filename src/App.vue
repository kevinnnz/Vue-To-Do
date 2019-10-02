<template>
  <div id="app">
    <Form />
  </div>
</template>

<script>
import Form from './components/todo/form.vue'

export default {
  name: 'app',
  components: {
    Form
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  width: 960px;
  margin: 0 auto;
}
</style>
