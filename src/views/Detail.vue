<template>
<div class="container">
  <div class="row">
    <div class="col-12 detail">
    <h2>{{apiData.title}}</h2>
    <img :src="apiData.image" alt="" srcset="">
    <transition name="fade"  appear>
    <p class="snippet">{{apiData.snippet}}</p>
    </transition>
    <transition name="fade" appear>
    <div :key="apiData.id" v-html="apiData.body">
    </div>
    </transition>
  </div>
  </div>
</div>
  
</template>

<script>
  export default {
    data() {
      return {
        url: 'http://sandbox.arabamd.com/news/',
        apiData: {}
      }
    },
    props: ['newId'],
    async mounted() {
      let fullUrl = this.url.trim() + this.newId;
      await fetch(fullUrl).then(async (response) => {
        this.apiData = await response.json();
      });
    }
  }
</script>

<style scoped lang="scss">
  .detail, h2,p{
    text-align: left;
    img{
      max-width: 100%;
      height: auto;
    }
    p, &~div, &~p{
      text-align: left;
    }
    .snippet{
      transition-delay: .6s;
    }
  }
  .fade-enter-active, .fade-leave-active {
    transition: opacity .7s, transform .5s;
    transition-delay: .8s;
  }
  .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
    opacity: 0;
    transform: rotateZ(-2deg) translateY(70px);

  }
</style>