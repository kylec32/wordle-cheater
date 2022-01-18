<template>
  <div id="app">
    <h1>Wordle Cheater</h1>
    <!-- <HelloWorld/> -->
    <OptionProvider/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import OptionProvider from './components/OptionProvider.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    OptionProvider
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
