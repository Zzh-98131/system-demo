<template>
  <div class="app-aside">
    <el-scrollbar>
      <el-menu
        :default-active="activeMenu"
        :collapse="isCollapse"
        :collapse-transition="false"
        mode="vertical"
      >
        <menu-item v-for="(i_menu, index) in menu1" :key="index" :opened="sidebar.opened" :menu="i_menu" />
      </el-menu>
    </el-scrollbar>
  </div>
</template>

<script>
  import { mapGetters } from 'vuex'

  import menuItem from './menu_item.vue'
  import menu from './menu.js'
  export default {
    name: 'side_nav_bar',
    components: {
      menuItem
    },
    data() {
      return {
        menu1: [
          {
            title: '监控管理',
            icon: 'monitor',
            children: [
              {
                title: '总览',
              },
              {
                title: '站点列表'
              },
              {
                title: '站点详情'
              },
              {
                title: '设备列表'
              },
              {
                title: '设备详情'
              },
              {
                title: '物联网卡'
              },
              {
                title: '统计分析',
                children: [
                  {
                    title: '运行数据'
                  },
                  {
                    title: '告警统计'
                  },
                  {
                    title: '站点发电量报表'
                  },
                  {
                    title: '设备发电量报表'
                  },
                  {
                    title: '流量统计'
                  }
                ]
              }
            ]
          },
          {
            title: '运维管理',
            icon: 'manage',
            children: [
              {
                title: '用户管理',
                children: [
                  {
                    title: '终端用户'
                  },
                  {
                    title: '后台用户'
                  },
                  {
                    title: '系统角色'
                  }
                ]
              },
              {
                title: '站点管理'
              },
              {
                title: '设备管理'
              },
              {
                title: '设备序列号管理'
              },
              {
                title: '设备软件管理',
                children: [
                  {
                    title: '固件管理'
                  },
                  {
                    title: '任务管理'
                  },
                  {
                    title: '设备调试'
                  }
                ]
              },
              {
                title: '物联网卡管理'
              },
              {
                title: '告警管理'
              }
            ]
          },
          {
            title: '系统管理',
            icon: 'setting',
            children: [
              {
                title: '操作日志'
              },
              {
                title: 'APP管理'
              },
              {
                title: '多语言管理'
              }
            ]
          }
        ]
      }
    },
    created() {
      console.log(menu)
    },
    methods: {

    },
    computed: {
      ...mapGetters([
        'sidebar',
      ]),
      activeMenu() {
        const route = this.$route
        const { meta, path } = route
        // if set path, the sidebar will highlight the path you set
        if (meta.activeMenu) {
          return meta.activeMenu
        }
        return path
      },
      variables() {
        return variables
      },
      isCollapse() {
        return !this.sidebar.opened
      }
    }
  }
</script>

<style lang="scss" scoped>
  /deep/.app-aside{
    /deep/.svg-icon{
      font-size: 20px;
    }
  }
</style>
