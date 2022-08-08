<template>
  <view class="container">
    <image  class="img" src="/static/img/pass_check_bg.jpg" />
    <view class="time">{{ time }}</view>
    <view class="name">赵小天</view>
    <view class="date">有效期：{{ date }}</view>
  </view>
</template>
 
<script>
  export default{
    data() {
      return {
        time: '2022-07-28 08:30:30',
        name: '',
        date: '2022-07-28',
        timer: null
      }
    },
    onShow() {
      this.intervalGetTime()
    },
    onHide() {
      this.clearIntervalGetTime()
    },
    methods: {
      // 获取时间
      getTime() {
        const date = new Date()
        const year = date.getFullYear()
        const month = (date.getMonth() + 1).toString().padStart(2,0)
        const day = date.getDate().toString().padStart(2,0)
        const hh = date.getHours().toString().padStart(2,0)
        const mm = date.getMinutes().toString().padStart(2,0)
        const ss = date.getSeconds().toString().padStart(2,0)
        this.time = year + '-' + month + '-' + day + ' ' + hh + ':' + mm + ':' + ss
        this.date = year + '-' + month + '-' + day
      },
      // 计时操作
      intervalGetTime() {
        this.timer = setInterval(() => {
          this.getTime()
        }, 1000)
      },
      // 清除计时器
      clearIntervalGetTime() {
        if (this.timer) {
          clearInterval(this.timer)
          this.timer = null
        }
      },
    }
  }
</script>

<style scoped lang="scss">
  .container {
    position: relative;
    .img {
      position: absolute;
      top: 0;
      left: 0;
      z-index: -2;
      width: 100vw;
      height: 100vh;
    }
    .time {
      width: 100%;
      text-align: center;
      margin: 0 auto;
      padding-top: 380rpx;
      font-size: 52rpx;
      font-weight: bold;
    }
    .name {
      position: absolute;
      left: 0;
      right: 0;
      top: 745rpx;
      text-align: center;
      width: 100%;
      font-size: 40rpx;
      color: #5a5a5a;
      background-color: #FFFFFF;
      font-weight: bold;
    }
    .date {
      text-align: center;
      width: 100%;
      margin-top: 480rpx;
      font-size: 38rpx;
      color: #5a5a5a;
    }
  }
  .title {
    color: #53C21D;
  }
</style>
