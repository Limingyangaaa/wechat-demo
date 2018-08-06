<template>
  <div id="app">
    <app-header :headerTitle="headerTitle" @webChange="webChange">
    </app-header>
    <app-nav :webCurrentIndex="webCurrentNum"></app-nav>
  </div>
</template>

<script>
import appHeader from '../../components/header.vue'
import appNav from '../../components/nav.vue'
export default {
  name: 'App',
  components: {
    appHeader,
    appNav
  },
  data () {
    return {
      headerTitle: '全部网点',
      webCurrentNum: '111'
    }
  },
  methods: {
    webChange (web) {
      this.webCurrentNum = web
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
* {
  padding:0; 
  margin:0;
}
</style>


<!-- <template>
  <div class="container" @click="clickHandle">
    <div class="message">{{msg}}</div>
    <click-counter></click-counter>
  </div>
</template>

<script>
  import ClickCounter from '@/components/click-counter'

  export default {
    components: {ClickCounter},
    data () {
      return {
        msg: 'hello'
      }
    },
    methods: {
      clickHandle () {
        this.msg = 'clicked1!'
      }
    }
  }
</script>

<style scoped>
.message {
  color: red;
  padding: 10px;
  text-align: center;
}
</style>

<template>
  <div class="container" @click="clickHandle('test click', $event)">
    <div class="userinfo" @click="bindViewTap">
      <img class="userinfo-avatar" v-if="userInfo.avatarUrl" :src="userInfo.avatarUrl" background-size="cover" />
      <div class="userinfo-nickname">
        <card :text="userInfo.nickName"></card>
      </div>
    </div>

    <div class="usermotto">
      <div class="user-motto">
        <card :text="motto"></card>
      </div>
    </div>

    <form class="form-container">
      <input type="text" class="form-control" v-model="motto" placeholder="v-model" />
      <input type="text" class="form-control" v-model.lazy="motto" placeholder="v-model.lazy" />
    </form>
    <a href="/pages/counter/main" class="counter">去往Vuex示例页面</a>
  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data () {
    return {
      motto: 'Hello World',
      userInfo: {}
    }
  },

  components: {
    card
  },

  methods: {
    bindViewTap () {
      const url = '../logs/main'
      wx.navigateTo({ url })
    },
    getUserInfo () {
      // 调用登录接口
      wx.login({
        success: () => {
          wx.getUserInfo({
            success: (res) => {
              this.userInfo = res.userInfo
            }
          })
        }
      })
    },
    clickHandle (msg, ev) {
      console.log('clickHandle:', msg, ev)
    }
  },

  created () {
    // 调用应用实例的方法获取全局数据
    this.getUserInfo()
  }
}
</script>

<style scoped>
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}

.usermotto {
  margin-top: 150px;
}

.form-control {
  display: block;
  padding: 0 12px;
  margin-bottom: 5px;
  border: 1px solid #ccc;
}

.counter {
  display: inline-block;
  margin: 10px auto;
  padding: 5px 10px;
  color: blue;
  border: 1px solid blue;
}
</style> -->