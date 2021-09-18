<template>
  <div id="app">
    <vue-select v-model="color" :options="colors" multiple />
  </div>
</template>

<script>
import VueSelect from './components/select/VueSelect'

export default {
  name: 'App',
  components: {
    VueSelect
  },
  data () {
    return {
      colors: ['red', 'green', 'blue'],
      color: ['red', 'blue']
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
  margin-top: 60px;
}
</style>
