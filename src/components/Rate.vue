<template>
  <div class="rate">
    <span>☆☆☆☆☆</span>
    <div class="hollow" :style="style">
      ★★★★★
    </div>


  </div>
</template>
<script>
  export default {
    created () {
      console.log(this.xingxing)
  },
    props: {
      // 设置传过来的集合默认为和校验

      xingxing: { type: [Number, String], default: '0' }

    },
    computed: {
      style () {
        // 要用``我也不知道为什么
        return `width:${this.xingxing / 2}em`
      }
    }

  }
</script>
<style scoped lang="scss">

  .rate {
    position: relative;
    display: inline-block;
    .hollow {
      position: absolute;
      display: inline-block;
      top: 0;
      left: 0;
      width: 0;
      overflow: hidden;
    }

  }

</style>
