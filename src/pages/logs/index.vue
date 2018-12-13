<template>
  <div>
    <swiper class="swiper"  previous-margin="30px"  next-margin="30px" interval="5000" duration="1000">
      <block v-for="(item, index) in books" :index="index" :key="key">
        <swiper-item>
          <div class="im1">
          <image :src="item.tupian" class="slide-image" mode="aspectFill"  />
          {{item.text}}</div>
        </swiper-item>
      </block>
    </swiper>


  </div>
</template>

<script>

export default {

  data () {
    return {
      logs: [],
      books: [
        {
          text: '平凡的世界',
          url: 'http://www.baidu.com',
          tupian: 'https://img3.doubanio.com/view/subject/l/public/s27449344.jpg'
        },
        {
          text: '活着',
          url: 'http://www.tencent.com',
          tupian: 'https://img3.doubanio.com/view/subject/l/public/s23836852.jpg'
        },
        {
          text: '解忧杂货店',
          url: 'http://www.baidu.com',
          tupian: 'https://img3.doubanio.com/view/subject/l/public/s27264181.jpg'
        }]
    }
  },
  methods: {

  }
}
</script>

<style scoped>
  .swiper {
    height: 600px !important;
  }
  image {
    height: 500px;
    width: 100%;
  }
</style>
