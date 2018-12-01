<template>
    <div>
      <name>获取评论</name>
<div    :key="index" @click="reply(index)"  v-for="(todo,index)in comments">

    </div>
</template>

<script>
  export default {
    name: 'comments',

    data () {
      return {
        userInfo: {},
        comments:[]
      }
    },
    props[isbn],
    mounted () {
      userInfo = StorageSync('userinfo')
      // 获取请求渲染数据
    },
    methods: {


      async getComments () {
        // 获取所有书
        const
          res = await get('http://localhost:8080/getComments', {
            isbn: this.isbn
          })
        if (res.code === 0 && res.data.title) {
          console.log('评论列表扫描成功', res)
        } else {
          // 添加图书
          showSuccess('评论失败')

          console.log('添加失败a', res)
        }
      }
    }
  }
</script>

<style scoped>

</style>
