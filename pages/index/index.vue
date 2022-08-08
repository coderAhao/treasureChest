<template>
  <view class="container">
    <u-button size="middle" color="#0ab8a2" @click="switchToPassCheck">通行证</u-button>
    <u-button size="middle" color="#0ab8a2" @click="switchToHealth">健康码</u-button>
    <u-button size="middle" color="#0ab8a2" @click="switchToPassTrip">行程码</u-button>
    <u-button size="middle" color="#0ab8a2" @click="switchToPlace">场所码</u-button>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        
      }
    },
    methods: {
      switchToPassCheck() {
        uni.$u.route('/pages/index/singlePage/passCheck')
      },
      switchToHealth() {
        uni.$u.route('/pages/index/singlePage/healthCode')
      },
      switchToPassTrip() {
        uni.$u.route('/pages/index/singlePage/tripCode')
      },
      switchToPlace() {
        uni.$u.route('/pages/index/singlePage/placeCode')
      }
    }
  }
</script>

<style scoped lang="scss">
  .container {
    padding-top: 100rpx;
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    .u-button {
      // flex: 1;
      width: 40%;
      margin: 10rpx auto;
    }
  }
</style>
