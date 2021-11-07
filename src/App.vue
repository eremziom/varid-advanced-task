<template>
  <div id="app">
    <h2>Varid Advanced Task</h2>
    <Form />
    <Table />
  </div>
</template>

<script>

import Table from './components/Table.vue';
import Form from './components/Form.vue'
export default {
  name: 'App',
  components: {
    Table,
    Form
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
