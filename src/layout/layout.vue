<template>
  <div :class="classObj" class="app-wrapper">
    <el-container>
      <Sidebar class="sidebar-container" />
      <el-container direction="vertical"  class="main-wrapper">
        <el-header :height="variables.header_height">
          <Header />
        </el-header>
        <el-main>
          <AppMain />
        </el-main>
        <el-footer>
          <Footer />
        </el-footer>
      </el-container>
    </el-container>
  </div>
</template>

<script>
  import { mapState } from 'vuex'

  import Sidebar from './components/nav_bar/side_nav_bar.vue'
  import Header from './components/app_header.vue'
  import AppMain from'./components/app_main.vue'
  import Footer from './components/app_footer.vue'

  import variables from '@/assets/styles/elements/variables.scss'
  export default {
    name: 'Layout',
    components: {
      Sidebar,
      Header,
      AppMain,
      Footer
    },
    computed: {
      ...mapState({
        sidebar: state => state.app.sidebar,
      }),
      classObj() {
        return {
          hideSidebar: !this.sidebar.opened,
        }
      },
      variables() {
        return variables
      }
    },
    methods: {

    }
}
</script>

<style lang="scss" scoped>
  @import '@/assets/styles/elements/variables.scss';

  *{
    padding: 0;
  }
  // .main-wrapper{
  //   width: 100%;
  //   height: 100%;
  //   min-height: 100%;
  //   transition: margin-left .28s;
  //   margin-left: $side_nav_bar_width;
  //   padding-bottom: $footer_height;
  //   position: relative;
  //   /* background: rgba(255, 85, 0, 0.1); */
  // }
  // .app-wrapper .el-aside{
  //   background: rgba(124, 82, 0, 0.1);
  //   height: 100%;
  //   position: fixed;
  //   left: 0;
  //   top: 0;
  //   z-index: 9999;
  // }
  .app-wrapper .el-header{
    /* background: rgba(0, 0, 0, 0.1); */
    position: fixed;
    top: 0;
    z-index: 9999;
    overflow: hidden;
    width: 100%;
  }
  .app-wrapper .el-main{
    /* background: rgba(255, 0, 0, 0.1); */
    margin: $header_height 0 0 0; /*$side_nav_bar_width*/
    min-height: calc(100vh - #{$header_height} - #{$footer_height}); /*最小高度=屏幕高度-(头部高度+尾部高度)*/
  }
  .app-wrapper .el-footer{
    background: rgba(150, 150, 150, 0.1);
    // position: absolute;
    width: 100%;
    bottom: 0;
  }
</style>
