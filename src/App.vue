<template>
  <div id="app">
    <PageTransition name="overlay-right-full">
      <router-view/>
    </PageTransition>
  </div>
</template>

<script>
import PageTransition from '@/components/PageTransition.vue'
export default {
  components:{
    PageTransition
  }
}
</script>

<style lang="scss">
$javascript : rgb(250,220,60);
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
