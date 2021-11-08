<template>
  <div id="app">
    <h2 class="mb-3">Varid Advanced Task</h2>
    <NavBar v-on:changeView="changeView"/>
    <Form v-if="formView" v-bind:currentData="currentData" v-on:changeView="changeView"/>
    <Table v-if="tableView" v-on:editData="editData"/>
  </div>
</template>

<script>

import Table from './components/Table.vue';
import Form from './components/Form.vue';
import NavBar from './components/NavBar.vue';
export default {
  name: 'App',
  components: {
    Table,
    Form,
    NavBar
  },
  methods:{
    editData(data){
      this.currentData = data;
      this.formView = true;
      this.tableView = false;
    },
    changeView(arg){
      if(arg === 1){
        this.tableView = true;
        this.formView = false;
        this.currentData = '';
      }
      if(arg === 2){
        this.tableView = false;
        this.formView = true;
        this.currentData = '';
      }
    }
  },
  data: function(){
    return{
      formView: false,
      tableView: true,
      currentData: '',
    }
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
  }
</style>
