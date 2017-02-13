<template>
  <div id="app">
    <hello></hello>
  </div>
</template>

<script>
import Hello from './components/Hello'

export default {
  name: 'app',
  components: {
    Hello
  }
}
</script>

<style>

body {
  margin: 0;
  padding: 0;
  background: #000;
}

#app {
  text-align: center;
  color: #8bd5ff;
}

</style>
