<template>
  <div>
  <div v-if="statues">
    <button @click="scan">扫码获取图书</button>
    {{scanresult.summary}}
  </div>
  <div v-else>
    <div class="head">
     <div class="head-i">
    <img :src="statues.image" class="footer-p1"
               style=" width:100px;  height: 100px;  "/>
     </div>
    <div class="head-t">
    书名：{{statues.title}}
      <div class="head-t">
        作者：{{statues.author}}
    </div>
      <div class="body">
        {{statues.summary}}
      </div></div>

  </div>
  </div></div>
</template>

<script>
  import card from '@/components/card'
import { showSuccess, get } from '@/utils/index'

export default {
    data () {
      return {
        motto: 'Hello World',
        userInfo: {},
        isbn: '',
        scanresult: {},
        statues: true
      }
    },

    components: {
      card
    },

    methods: {
      async addBook (isbbn) {
        const
          res = await get('http://localhost:8080/addBOOK', {
            isbn: this.isbn,
            openid: this.userInfo.openid
          })
        if (res.code === 0 && res.data.title) {
          showSuccess('添加成功')
          console.log('添加成功', res)
        } else {
          // 添加图书
          showSuccess('添加失败a')
          this.statues = !this.statues
          this.scanresult = res
          console.log(this.scanresult)
          console.log('添加失败a', res)
        }
      },
      scan () {
        wx.scanCode({
          success: (res) => {
            this.isbn = res.result
            console.log('扫码的值', this.isbn)
            this.addBook()
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
    width: 128 rpx;
    height: 128 rpx;
    margin: 20 rpx;
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
