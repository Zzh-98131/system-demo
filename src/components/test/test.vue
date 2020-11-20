<template>
  <div>
    <el-link type="primary" @click="back" icon="el-icon-back">回到首页</el-link>
    <div class="test_wrapper">
      <el-button @click="btnClick">属性可观测</el-button>
      <div class="show_box">{{ show_1 }}</div>
      <el-button @click="toabc">修改属性a</el-button>
    </div>
    <div class="test_wrapper">
      <p>标题：异步</p>
      <div style="border: #000000 1px dotted;">
        <p>数据展示区</p>
        {{ show_2 }}
      </div>
      <el-button @click="toAsync">点击执行异步</el-button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'test',
  data() {
    return {
      car: {},
      val: 3000,
      show_1: null,
      show_2: '异步数据展示'
    }
  },
  created() {
    this.getData()
  },
  methods: {
    toAsync() {
      function returnPromise(val) {
        return new Promise((resolve, reject) => {
          setTimeout(() => {
            resolve(val * 2)
          }, 2 * 1000)
        })
      }
      async function timeout() {
        let result = await returnPromise(40)
        console.log(result)
      }
      function console_666() {
        console.log('666')
      }
      console.log('1')
      timeout()
      console_666()
      console.log('2')
    },
    btnClick() {
      this.show_1 = this.car.price
      this.car.price = 5000
    },
    getData() {
      Object.defineProperty(this.car, 'price', {
        enumerable: true,
        configurable: true,
        get(){
          console.log('price属性被读取了')
          return this.val
        },
        set(newVal){
          console.log('price属性被修改了')
          this.val = newVal
        }
      })
    },
    toabc() {
      this.abc(this.car, '还没改呢', 200)
    },
    abc(object, name, value) {
      object.name = '已被修改'
      object.value = -99999
      alert(object.name + object.value + ' ' + Object.keys(object))
      // if ( typeof Object.keys(object)[0] === 'string') alert(`${Object.keys(object)[0]}是啊是啊`)
    },
    back() {
      this.$router.go(-1)
    }
  }
}
</script>

<style scoped>
  .test_wrapper{
    width: 98%;
    padding: 5px;
    margin: 10px 0;
    background-color: rgba(255, 170, 0, 0.1);
    border: rgba(255, 170, 0, 0.5) 1px solid;
  }
</style>
