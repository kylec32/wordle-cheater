<template>
  <div id="app">
    <div class="page-title">Wordle Cheater</div>
    <br/>
    <br/>
    <OptionProvider/>
  </div>
</template>

<script>
import OptionProvider from './components/OptionProvider.vue'

export default {
  name: 'App',
  components: {
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
  margin-top: 20px;
  width: 100%;
}
.page-title {
  font-size:55px;
  border-bottom: 1px black;
  border-bottom-style: solid;
  width: 100%;
  margin-left: auto;
  margin-right: auto;
}
</style>
