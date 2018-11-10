<template>
  <div   class="progressbar">
  进度条
    <progress  :percent="percent" activeColoe="pink"  color="#4AACF1" ></progress>
    <p>{{year}}年已经过了{{days}}天{{percent}}</p>
  </div>
</template>

<script>
  export default {
  method: {
    // 算闰年非闰年
      isLeapYear () {
        const year = new Date().getFullYear()
        if (year % 400 === 0) {
          return true
        } else if (year % 4 === 0 && year % 100 !== 0) {
          return true
        } else {
          return false
        }
      },
      getDayOfYear () {
        return this.isLeapYear() ? 366 : 365
      }
  },
  computed: {
      year () {
        return new Date().getFullYear()
      },
      days () {
        let start = new Date()
        start.setMonth(0)
        start.setDate(1)
        // start今年第一天
        let offset = new Date().getTime() - start.getTime()
        // 时间戳毫秒
        return parseInt(offset / 1000 / 60 / 60 / 24) + 1
      },
      percent () {
        // 小数点后面保留一位
        return (this.days() * 100 / getDayOfYear()).toFixed(1)
      }
  }
  }
</script>

<style  scoped lang="scss">
  .progressbar{
    width:100% ;

    progress{
      margin-bottom: 10px;

  }}

</style>

