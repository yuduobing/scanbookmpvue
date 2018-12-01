<template>
  <div>
    <div v-if="statues">
      <button @click="scan">扫码获取图书</button>

      <Rate v-bind:xingxing="value"></Rate>
    </div>
    <div v-else>
      <div class="all">
        <div class="head">
          <div class="head-i">
            <img :src="scanresult.image" class="footer-p1"
                 style=" width:60px;  height:80px;  "/>
          </div>
          <div class="head-t">
            <div style="color: #737373;font-size: 13px;">
              书名：{{scanresult.title}}<br/></div>
            <div class="head-author">
              作者：{{scanresult.author}}
            </div>
          </div>
        </div>

        <div class="body">概述<br/>
          <div style="padding: 10px;">
            {{scanresult.summary}}
          </div>
        </div>


        <div class="bd">
          评论
        </div>


      </div>

    </div>

  </div>
</template>

<script>
  import card from '@/components/card'
import { showSuccess, get } from '@/utils/index'
import Rate from '@/components/Rate'

export default {
    data () {
      return {
        value: '5',
        motto: 'Hello World',
        userInfo: {},
        isbn: '',
        scanresult: {},
        statues: true
      }
  },

    components: {
      card,
      Rate
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
          showSuccess('添加成功a')
          this.statues = !this.statues
          // 存储扫码的值

          this.scanresult = res
          wx.setStorageSync('books', this.scanresult)
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

<style scoped lang='scss'>

  .all {
    position: fixed;
    min-height: 100%;
    padding: 8px;
    padding-top: 20px;
    background-color: #0087D9;
    width: 100%;
    margin: 0 auto;
    .head {

      background-color: white;
      width: 100%;
      border-radius: 15px;
      overflow: hidden;
      height: 130px;
      .head-i {
        margin: 14px;
        float: left;
      }
      .head-t {
        margin: 34px;
        float: left;

      }

    }

    .body {
      width: 100%;
      border-radius: 15px;

      margin-top: 10px;

      background-color: white;

      display: -webkit-box;
      overflow: hidden;
      text-overflow: ellipsis;
      word-break: break-all;
      -webkit-box-orient: vertical;
      -webkit-line-clamp: 5;

    }
  }

  .bd {
    width: 100%;
    border-radius: 15px;
    background-color: white;
    margin-top: 20px;
  }

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
