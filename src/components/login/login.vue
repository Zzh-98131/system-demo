<template>
  <div>
    <!-- <div class="bg" /> -->
    <div class="wrapper">
      <div id="loginLogo" :class="{roll:isRoll==true}" v-if="isLogo">
        <img style="box-shadow: 10px 10px 20px #937b51; border-radius: 100px;" src="../../assets/img/orange.png" @click="toLoginCard" @mouseenter="scroll" @mouseleave="stop"/>
      </div>
      <div id="transblock" :class="{trans:isguodu==true}" v-if="isTransition"></div>
      <div id="loginCard" v-if="isLogin">
        <el-card>
          <div slot="header" class="cardHeader">
            <span><svg-icon icon-class="orange"></svg-icon>CL律师事务所</span>
            <el-link type="primary" @click="reload" style="float: right;" :underline="false"><i class="el-icon-right el-icon--right"></i></el-link>
          </div>
          <el-form label-width="60px">
            <el-form-item label="用户名">
              <el-input clearable placeholder="请输入用户名" v-model="userName"></el-input>
            </el-form-item>
            <el-form-item label="密码">
              <el-input placeholder="请输入密码" clearable v-model="passWord" show-password></el-input>
            </el-form-item>
            <el-button style="width: 100%;" type="primary" @click="clickHandle">{{ msg }}</el-button>
          </el-form>
        </el-card>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data() {
    return {
      msg: '登录',
      userName: '',
      passWord: '',
      isLogo: true,
      isTransition: false,
      isguodu: false,
      isLogin: false,
      isRoll: false,
      timer: null,
      timer1: null
    }
  },
  mounted() {
    this.$once('hook:beforeDestroy', () => {
      clearInterval(this.timer)
      clearTimeout(this.timer1)
      this.timer = null
      this.timer1 = null
    })
  },
  methods: {
    stop() {
      clearInterval(this.timer)
      clearTimeout(this.timer1)
      this.isRoll = false
      this.timer = null
    },
    scroll() {
      document.getElementById('loginLogo').style.marginTop = '14%'
      this.isRoll = !this.isRoll
      var that = this
      setTimeout(function() {
        document.getElementById('loginLogo').style.marginTop = '15%'
        // that.isRoll = !that.isRoll
      }, 400) // 滚动上去的时间

      this.timer = setInterval(() => { // 加入定时器使其循环
        document.getElementById('loginLogo').style.marginTop = '14%'
        this.isRoll = !this.isRoll
        var that = this
        that.timer1 = setTimeout(function() {
          document.getElementById('loginLogo').style.marginTop = '15%'
          // that.isRoll = !that.isRoll
        }, 400) // 滚动上去的时间
      }, 800) // 时间 = 滚动上去的时间 + 滚动下来的时间
    },
    toLoginCard() {
      this.stop()
      this.isLogo = false
      this.isTransition = !this.isTransition
      var that = this
      that.timer = setTimeout(function() {
        document.getElementById('transblock').style.width = '20%'
        document.getElementById('transblock').style.height = '264px'
        document.getElementById('transblock').style.opacity = 0.8
        that.isguodu = !that.isguodu
        that.timer1 = setTimeout(function() {
          that.isTransition = !that.isTransition
          that.isguodu = !that.isguodu
          that.isLogin = true
        },500)
      },100)
    },
    reload() {
      location.reload()
    },
    clickHandle() {
      this.$router.push({ path: '/index' })
    }
  }
}
</script>

<style scoped>
  .bg{
    width: 100%;
    height: 760px;
    overflow: hidden;
    /* filter: blur(4px); */
    /* background-repeat: repeat; */
    /* background-image: url(../../assets/img/bg2.jpg); */
    background-color: #ffd58c;
    /* background-size: 100% 100%; */
  }
  .wrapper{
    text-align: center;
    width: 100%;
    height: 100%;
    background-color: #ffd58c;
    position: fixed;
    top: 0;
  }
  #loginLogo{
    margin: 15% auto;
    transition: all .4s; /*滚动回来的时间*/
  }
  #loginLogo :hover{
    cursor: pointer;
  }
  .roll{
    transition: all .4s; /*滚动上去的时间*/
  }
  #transblock{
    width: 0%;
    height: 0px; /*loginCard的高*/
    margin: 15% auto;
    opacity: 0;
    border-radius: 5px;
    background: rgba(255, 255, 255, 1);
  }
  .trans{
    transition: all .5s;
  }
  #loginCard{
    width: 20%;
    margin: 15% auto;
  }
  .cardHeader{
    text-align: center;
  }
  .el-card{
    opacity: 1;
  }
</style>
