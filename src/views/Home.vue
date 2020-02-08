<template ref="home-page">
  <div @load.once="getParagraphs" class="container">
    <div v-if="apiData != undefined" class="row">
      <a v-for="(data,i) in apiData" class="v-padding-10" :key="data.id" @click="choochoo(i)"
        :class="data.isFeatured ? 'col-12 col-lg-12' : 'col-12 col-lg-4'">
        <div class="each-new-card">
          <img :src="data.image" alt="" class="new-image" srcset="">
          <div class="image-desc">
            <h2>{{data.title}}</h2>
            <p :class="{'haveSpace' :data.isFeatured}">{{data.snippet}}</p>
          </div>
        </div>
      </a>
    </div>
    <div v-else class="">Loading</div>
  </div>
</template>

<script>
  // @ is an alias to /src
  // import HelloWorld from '@/components/HelloWorld.vue'
  import router from '../router/index';

  export default {
    name: 'home',
    data() {
      return {
        url: 'http://sandbox.arabamd.com/news',
        apiData: {},
      }
    },
    methods: {
      async getNews() {
        await fetch(this.url).then(async (response) => {
          this.apiData = await response.json();
        });
      },
      choochoo(i){
        i++;
        router.push({ path:`/detail/${i}`, props: { newId: i.toString() } })
      }
    },
    mounted() {
      this.getNews();
    },
    updated() {
      window.onload = (() => {
        let descriptions;
        if(window.screen.width > 768){
          descriptions = document.querySelectorAll('.image-desc p:not(.haveSpace)');
        }
        else{
          descriptions = document.querySelectorAll('.image-desc p');
        }
        descriptions.forEach((el) => {
          // support for smaller height screens to prevent overflow (:
          el.innerText.length > 130 ? el.innerText = el.innerText.substr(0, 130) + '...' : el.innerText;
        })
      })();
    },
  }
</script>

<style scoped lang="scss">
@mixin desktop {
  @media (max-width: 960px) { @content; }
}
  .each-new-card {
    position: relative;
    overflow: hidden;
    cursor: pointer;
    text-align: left;
    border-radius: 7px;

    &:hover .image-desc {
      bottom: 0;
      opacity: 1;
      padding: 5px 10px;
    }

    &::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 5px;
    }

    &:hover {
      box-shadow: 1px 2px 10px 5px rgba(0, 0, 0, 0.065);
    }

    h2 {
      font-size: 16px;
      margin: .3rem 0;
      word-break: break-word;
    }

    .image-desc {
      position: absolute;
      bottom: -100px;
      opacity: 0;
      width: 100%;
      padding: 0 10px 0 0;
      transition: opacity .4s cubic-bezier(0.075, 0.82, 0.165, 1),
        bottom .4s cubic-bezier(0.075, 0.82, 0.165, 1),
        padding .5s cubic-bezier(0.075, 0.82, 0.165, 1);
      background-color: rgba(0, 0, 0, 0.8);
      color: #fff;
      font-size: 13px;
      @include desktop{
        bottom: 0;
        opacity: 1;
        padding: 5px 10px;
        height: 100%;
      }
    }

    .new-image {
      width: 100%;
      display: block;
      height: auto;
    }
  }

  .v-padding-10 {
    padding-top: 10px;
    padding-bottom: 10px;
  }
</style>