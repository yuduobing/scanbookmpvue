<template>
  <div>
    <div class="container1">
      <div class="head">
        <open-data class="person" type="userAvatarUrl"></open-data>

        <div class="person-name">欢迎你:
          <open-data type="userNickName"></open-data>
        </div>
      </div>
      <!-- 需要使用 button 来授权登录 -->


      <button v-if="statues" open-type="getUserInfo" @getuserinfo="bindGetUserInfo" @click="getUserInfo1">获取权限</button>
      <button @click="login">获取openid</button>
      <YearProgress></YearProgress>
    </div>
  </div>
</template>
<script>
  import YearProgress from '../../components/YearProgress'
  export default {
    components: {
      YearProgress
    },
    data () {
      return {
        statues: true

      }
    },
    created () {

    },
    onload () {
      // 这个时候 不行，可能与生命周期有关系
      // this.getSetting()
    },

    onShow () {
      const a = (wx.getStorageSync('userInfo') || [])
      console.log(a)
      if (a) {
        this.statues = !this.statues
      } else { console.log('用户还未登陆') }
    },
    mounted () {
      // 一进来看看用户是否授权过

  },
    methods: {
      login () {
        wx.login({
          success: function (res) {
            console.log('code:' + res.code)
            // 发送请求
            wx.request({
              url: 'http://localhost:8080/sign', // 改成自己的服务器地址
              data: {
                code: res.code, // 上面wx.login()成功获取到的code
                operFlag: 'getOpenid'
              },
              header: {
                'content-type': 'application/json' // 默认值
              },
              success: function (res) {
                console.log(res)
              }
            })
          }
        })
      },
      getSetting () {
        wx.getSetting({
          success: function (res) {
            if (res.authSetting['scope.userInfo']) {
              wx.getUserInfo({
                success: (res) => {
                  wx.setStorageSync('userInfo', res.userInfo)
                  console.log(res.userInfo)
                  // 用户已经授权过
                  console.log('用户已经授权过')
                }
              })
            } else {
              console.log('用户还未授权过')
            }
          }
        })
      },
      getUserInfo1 () {
        console.log('click事件首先触发')
        // 判断小程序的API，回调，参数，组件等是否在当前版本可用。  为false 提醒用户升级微信版本
        // console.log(wx.canIUse('button.open-type.getUserInfo'))
        if (wx.canIUse('button.open-type.getUserInfo')) {
          // 用户版本可用
        } else {
          console.log('请升级微信版本')
        }
      },
      bindGetUserInfo (e) {
        // console.log(e.mp.detail.rawData)
        if (e.mp.detail.rawData) {
          // 用户按了允许授权按钮
          console.log('用户按了允许授权按钮')
          this.statues = !this.statues
        } else {
          // 用户按了拒绝按钮
          console.log('用户按了拒绝按钮')
        }
      }
    }
  }
</script>

<style scoped lang='scss'>
  .container1 {
    margin: 0 auto;
    padding: 8px;
    font-size: 16px;
    .head{


    .person {
      width: 88rpx;
      height: 88rpx;
      margin-left:40rpx;

      border-radius: 50%;

      display: inline-block;
      overflow: hidden;
    }
    .person-name {
      margin-top: 30rpx;
       float: right;
    }}
  }
</style>
