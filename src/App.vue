<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/mask.jpeg">
      <console-line
        v-for="line in lines"
        v-bind:key="line.id"
        v-bind:line="line.text"
      ></console-line>

      <div v-if="showInput">
        <div v-for="(code, index) in codes" :key="code.message">
          <span>Code {{ code.id }}: <input v-on:keyup="validateCodes" v-model="inputs[index]"></span> 
          <span style="width:40px;margin-left:5px" v-show="inputs[index]===code.text">correct code</span>
        </div>
      </div>

      <div v-show="validCodes">
        <console-line v-bind:line="congrats"></console-line>
      </div>
  </div>
</template>

<script>
import ConsoleLine from './components/ConsoleLine.vue'
var waitTime = 5000;
var const_lines = [
  { id: 1, text: 'your birthday has been hacked by project zorgo' },
  { id: 2, text: 'to get your presents you must do some ninja spy work' },
  { id: 3, text: 'there will be a series of codes below'},
  { id: 4, text: 'enter the codes correctly to get your next present'},
  { id: 5, text: 'instructions are located in an envelope'},
  { id: 6, text: 'taped under the desk in your fathers office'}
];
var congrats_message = 'congratulations. your present is located in ???'

var lines= [];

var inputs= [];

var codes = [
  { id: 1, text: '1607' },
  { id: 2, text: '2222' },
  { id: 3, text: '3333' },
  { id: 4, text: '4444' }
];

async function addLines(app) {
  for (var i in const_lines) {
    lines.push(const_lines[i]);
    await new Promise(r => setTimeout(r, waitTime));
  }
  app.showInput=true;
}

export default {
  name: 'App',
  el: '#app',
  components: {
    ConsoleLine
  },
  data: function() {  
    return { 
      lines: lines,
      showInput: false,
      codes: codes,
      inputs: inputs,
      validCodes: false,
      congrats: congrats_message
    }
  },
  methods: {
    validateCodes: function() {
      if (inputs.length === codes.length) {
        var valid = true;
        var i;
        for (i = 0; i < codes.length; i++) {
          if (codes[i].text != inputs[i])
            valid = false;        
        }
        this.validCodes = valid;
        if(valid === true)
          this.validCodes=true;
      }
    }
  },
  created: function () {
    addLines(this);
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #4ceb34;
  font-size: 14px;;
  background-color: black;
}
</style>