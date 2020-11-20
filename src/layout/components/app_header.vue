<template>
  <div class="title-bar">
    <div class="left">
      <Hamburger class="hamburger-container" :isActive="sidebar.opened" @toggleClick="toggleSideBar" />
      <svg-icon icon-class="orange" />
      <span class="title-word">Orange!</span>
    </div>

    <div class="right">
      <svg-icon icon-class="user" />
    </div>
  </div>
</template>

<script>
  import { mapGetters } from 'vuex'
  import Hamburger from '@/components/public/Hamburger/hamburger.vue'
  export default {
    name: 'app_header',
    components: {
      Hamburger
    },
    computed: {
      ...mapGetters([
        'sidebar',
      ])
    },
    methods: {
      toggleSideBar() {
        this.$store.dispatch('app/toggleSideBar')
      }
    }
  }
</script>

<style lang="scss" scoped>
  @import '@/assets/styles/elements/variables.scss';

  .title-bar{
    height: $header_height;
    background-color: $header_background_color;
    overflow: hidden;
    color: #fffdeb;
    position: relative;

    .hamburger-container{
      line-height: $header_height;
      height: 100%;
      float: left;
      cursor: pointer;
      transition: background 0.3s;
      -webkit-tap-highlight-color: transparent;

      &:hover {
        background: rgba(0, 0, 0, 0.025);
      }
    }
    .title-word{
      font-size: 50px;
    }
    .left{
      float: left;
      height: 100%;
      border: #000000 1px solid;
    }
    .right{
      float: right;
      width: 180px;
      border: #000000 1px solid;
      height: 100%;
    }
    .svg-icon{
      font-size: 50px;
    }
  }
</style>
