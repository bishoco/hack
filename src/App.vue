<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/mask.jpeg"> -->
      <console-line
        v-for="line in lines"
        v-bind:key="line.id"
        v-bind:line="line.text"
      ></console-line>
  </div>
</template>

<script>
import ConsoleLine from './components/ConsoleLine.vue'

export default {
  name: 'App',
  el: '#app',
  components: {
    ConsoleLine
  },
  data: function() {  
    return { 
      lines: lines
    }
  }
}

var lines = [
  { id: 1, text: 'My journey with Vue' },
  { id: 2, text: 'Blogging with Vue' },
  { id: 3, text: 'Why Vue is so fun' }
];
lines.push({ id: 4, text: 'HA' });

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #4ceb34;
  margin-top: 60px;
  background-color: black;
}
</style>