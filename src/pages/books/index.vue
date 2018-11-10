<template>
 <div>
   <button  @click="scan">扫码获取图书</button>
  </div>
</template>

<script>
  import card from '@/components/card'
  import {showSuccess} from '@/utils/index'

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
      scan () {
        wx.scanCode({
          success : (res) => {
            console.log("扫码的值", res.result)
          },
          fail: (res) => {
            console.log(res)
          }
        })
      },
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
                console.log('登陆成功', res)

                wx.setStorageSync('userInfo', res.userInfo)
                showSuccess('登陆成功')
              },
              fail: (res) => {
                console.log('登陆失败', res)
                showSuccess('登录失败')
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
</style>
