<template>
  <view class="container">
    <view class="empty"></view>
    <image class="img" src="/static/img/health_bg.jpg" />
    <view class="scroll-container">
      <u-notice-bar :text="noticeText" icon="" bgColor="#fffbe" color="#d36e36" fontSize="20" duration="5000">
      </u-notice-bar>
    </view>
    <view class="time">{{ time }}</view>
    <view class="trip" @click="switchToTripCode"></view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        time: '07-28 08:30:30',
        name: '',
        noticeText: '若您有近7天中高风险地区旅居史(含境外)请及时更新信息和风险报备。',
        timer: null,
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
        const month = (date.getMonth() + 1).toString().padStart(2, 0)
        const day = date.getDate().toString().padStart(2, 0)
        const hh = date.getHours().toString().padStart(2, 0)
        const mm = date.getMinutes().toString().padStart(2, 0)
        const ss = date.getSeconds().toString().padStart(2, 0)
        this.time = month + '-' + day + ' ' + hh + ':' + mm + ':' + ss
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
      switchToTripCode() {
        uni.$u.route('/pages/index/singlePage/tripCode')
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

    .scroll-container {
      position: absolute;
      top: 370rpx;
      width: 100vw;
      // height: 100rpx;
      // background-color: rgba(0,0,0,.2);
    }

    .time {
      position: absolute;
      left: 50%;
      margin-left: -45%;
      top: 495rpx;
      width: 90%;
      height: 120rpx;
      line-height: 120rpx;
      // background-color: rgba(0,0,0,.2);
      background-color: #FFFFFF;
      text-align: center;
      font-size: 88rpx;
      font-weight: bold;
    }

    .trip {
      position: absolute;
      z-index: 2;
      width: 100vw;
      height: 100rpx;
      bottom: 0;
    }
  }
</style>
