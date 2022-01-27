<template>
  <div id="app">    
    <TodoMan msg="TodoMan"/>
  </div>
</template>

<script>
import TodoMan from './components/TodoMan.vue'


export default {
  name: 'App',
  components: {
    TodoMan
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
