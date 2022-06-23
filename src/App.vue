<template>
  <div id="app">
    <img class="logo" alt=" logo" src="./assets/logo.svg">
    <TipCalculator/>
  </div>
</template>

<script>
import TipCalculator from './components/TipCalculator.vue'

export default {
  name: 'App',
   
  components: {
    TipCalculator
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Space+Mono:wght@700&display=swap');
*{
  padding: 0px;
  margin: 0px;
  box-sizing: border-box;
  
}
#app {
  font-family: 'Space Mono', monospace;
  font-weight: 700;
  text-align: center;
  padding-top: 40px;
  font-size: 24px;  
}
@media ( max-width:1000px) {
  .logo{
    margin: auto 210px auto;
    text-align: center;
    justify-content: center;
  }
}
</style>
