<template>
  <div id="app">
    <container></container>
  </div>
</template>

<script>
import Container from './components/Container'

export default {
  name: 'app',
  components: {
    Container
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>