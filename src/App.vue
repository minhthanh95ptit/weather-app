<template>
  <div id="app">
   
    <Weather/>
  </div>
</template>

<script>
import Weather from './components/Weather.vue'

export default {
  name: 'App',
  components: {
    Weather
  }
}
</script>

<style>
  *{
      margin: 0;
      padding: 0;
      box-sizing: border-box;
  }

  html,body{
      width: 100%;
      height: 100%;
  }
  
  #app{
    width: 100%;
    height: 100%;
    background-color: darkseagreen
  }
</style>
