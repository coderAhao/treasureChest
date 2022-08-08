<template>
  <view class="container">
    <view class="empty"></view>
    <image class="img" src="/static/img/trip_bg.jpg" />
    <view class="date">更新于：{{ date }}</view>
    <image class="arrow" src="/static/img/scale_arrow.jpg"></image>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        date: '2022.07.28 08:30:30',
      }
    },
    onShow() {
      this.getTime()
    },
    methods: {
      // 获取时间
      getTime() {
        const date = new Date()
        const year = date.getFullYear()
        const month = (date.getMonth() + 1).toString().padStart(2, 0)
        const day = date.getDate().toString().padStart(2, 0)
        const hh = date.getHours().toString().padStart(2, 0)
        const mm = date.getMinutes().toString().padStart(2, 0)
        const ss = date.getSeconds().toString().padStart(2, 0)
        this.date = year + '.' + month + '.' + day + ' ' + hh + ':' + mm + ':' + ss
      }
    }
  }
</script>

<style scoped lang="scss">
  .container {
    position: relative;
    height: 100vh;

    .empty {
      width: 100vh;
      height: 70rpx;
      background-color: #b0b0b0;
    }

    .img {
      position: absolute;
      top: 70rpx;
      left: 0;
      z-index: -2;
      width: 100vw;
      height: calc(100vh - 70rpx);
    }

    .date {
      position: absolute;
      top: 560rpx;
      width: 100%;
      text-align: center;
      font-size: 30rpx;
      color: #a4a5a9;
    }
    .arrow {
      position: absolute;
      top: 660rpx;
      width: 280rpx;
      height: 280rpx;
      left: 50%;
      margin-left: -140rpx;
      animation: scaleWidth 1.5s linear infinite;
    }
    @keyframes scaleWidth {
      0% {
        transform: scale(1);
      }
      50% {
        transform: scale(1.3);
      }
      100% {
        transform: scale(1);
      }
    }
  }
</style>
