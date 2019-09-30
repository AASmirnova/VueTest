<template>
  <div id="app">
    <!--<HelloWorld msg="Welcome to Your Vue.js App"/>-->
    <Search/>
  </div>
</template>



<script>
//import HelloWorld from './components/HelloWorld.vue'
import Search from './components/Search.vue'

export default {
  name: 'app',
  components: {
    Search
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
    ul {
      padding: 0;
    }
    li {
      list-style-type: none;
    }
</style>
