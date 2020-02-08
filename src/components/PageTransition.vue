<template>
  <div>
    <transition :name="transition">
      <slot></slot>
    </transition>
    <div class="overlay-right"></div>
  </div>
</template>

<script>
export default {
  props: ['name'],
  data () {
    return {
      transition: 'overlay-right-full',
    }
  },
  created () {
    this.$router.beforeEach((to, from, next) => {
      this.transition = to.meta.transition
        ? to.meta.transition
        : this.$props.name
      next()
    })
  },
}
</script>

<style lang="scss">
@mixin mid {
  @media (max-width: 580px) { @content; }
}
$javascript : rgb(250,220,60);
.overlay-right-full-enter-to ~ .overlay-right {
  width: 0;
}
.overlay-right-full-enter-to ~ .overlay-right::after{
  opacity: 0;
}

.overlay-right-full-leave-active ~ .overlay-right {
  transition-timing-function: ease;
}

.overlay-right-full-enter ~ .overlay-right,
.overlay-right-full-enter-active ~ .overlay-right,
.overlay-right-full-enter-to ~ .overlay-right {
  transition-duration: unset !important;
  width: 100vw;
}
.overlay-right-full-enter ~ .overlay-right::after,
.overlay-right-full-enter-active ~ .overlay-right::after,
.overlay-right-full-enter-to ~ .overlay-right::after {
  transition-duration: unset !important;
  opacity: 1;
}

.overlay-right-full-enter-active,
.overlay-right-full-leave-active {
  transition-duration: 350ms;
}
.overlay-right {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  z-index: 4;
  width: 0;
  background: #222;
  transition-duration: 350ms;
}
.overlay-right::after{
    content: "Ozgur Seyidoglu";
    white-space: nowrap;
    color: $javascript;
    position: absolute;
    font-weight: 900;
    top: 50%;
    font-size: 35px;
    left:50%;
    transform: translate(-50%,-50%);
    background: transparent;
    z-index: 1;
    opacity: 0;
    transition: all .6s ease-in;
    @include mid{
      white-space:normal;
    }
}
.overlay-right::before{
    content: '';
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgb(37,39,43);
    top: 0;
    border-top: 3px solid $javascript;
    padding: 0px;
    left: 0;
    right: 0;
    bottom: 0;
    transition: all .6s ease-out;
}


.overlay-right-enter ~ .overlay-right,
.overlay-right-leave-to ~ .overlay-right {
  width: 0;
}
.overlay-right-enter ~ .overlay-right::after,
.overlay-right-leave-to ~ .overlay-right::after {
  opacity: 0;
}

.overlay-right-enter-active ~ .overlay-right,
.overlay-right-leave-active ~ .overlay-right {
  width: 100vw;
}
.overlay-right-enter-active ~ .overlay-right::after,
.overlay-right-leave-active ~ .overlay-right::after {
  opacity: 1;
}


.overlay-right-enter-active ~ .overlay-right {
  transition-timing-function: ease-in;
}

.overlay-right-leave-active ~ .overlay-right {
  transition-timing-function: ease-out;
}

.overlay-right-enter-active,
.overlay-right-leave-active {
  transition: opacity 300ms width 350ms;
}
</style>
