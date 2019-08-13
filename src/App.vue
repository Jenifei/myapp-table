<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to myapp-table"/>
    <hr/>
    <!-- <MyTable></MyTable> -->
    <TableApp></TableApp>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import TableApp from './components/TableApp.vue'
// import MyTable from './components/MyTable.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    TableApp,
    // MyTable,
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
