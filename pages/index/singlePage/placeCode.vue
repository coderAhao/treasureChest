<template>
  <view class="container">
    <view class="empty"></view>
    <view class="input-container" v-if="!showText">
      <u-input v-model="formData.location"></u-input>
      <u-input v-model="formData.area"></u-input>
    </view>
    <view class="show-text" :class="!formData.area ? 'hidden-area' : ''" v-else>
      <view class="location">{{formData.location}}</view>
      <view class="area">{{formData.area}}</view>
    </view>
    <view class="show-or-hidden" @click="showText = !showText"></view>
    <image class="img" v-if="hiddenBg" src="/static/img/place_code_bg.jpg" />
    <image class="img" v-else :style="{'height':screenHeight + 'px'}" src="/static/img/place_code_bg.jpg" />
    <view class="date">{{ date }}</view>
    <view v-show="hiddenBg" class="collection-time time">{{collectionDate}}</view>
    <view v-show="hiddenBg" class="result-time time">{{collectionDate}}</view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        date: '2022年07月28日 08:30:30',
        collectionDate: '7月29日',
        formData: {
          location: '江苏省苏州市相城区青龙港路286号',
          area: '相城区',
        },
        showText: true,
        screenHeight: 760,
        showOrHidden: false,
        distance: 250,
        hiddenBg: true,
      }
    },
    mounted() {
      // 键盘弹起隐藏保存按钮,否则按钮会被顶上来
      uni.onKeyboardHeightChange(res => {
        this.hiddenBg = res.height == 0 ? true : false 
        console.log(res);
      })
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
        this.date = year + '年' + month + '月' + day + '日' + ' ' + hh + ':' + mm + ':' + ss
        if (day == '01') {
          this.collectionDate = date.getMonth() + '月' + '30' + '日'
        } else {
          this.collectionDate = date.getMonth() + 1 + '月' + (date.getDate() - 1).toString().padStart(2, 0) + '日'
        }
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

.input-container,.show-text {
  position: absolute;
  font-size: 34rpx;
}
.show-text {
  top: 235rpx;
  left: 170rpx;
  .location {
    font-weight: bold;
    margin-bottom: 10rpx;
  }
  .area {
    font-size: 26rpx;
    color: #fda923;
  }
}
.hidden-area {
  top: 260rpx;
}
.input-container {
  top: 200rpx;
  left: 160rpx;
}
.show-or-hidden {
  width: 120rpx;
  height: 120rpx;
  position: absolute;
  left: 20rpx;
  top: 220rpx;
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
      top: 725rpx;
      width: 100%;
      text-align: center;
      font-size: 32rpx;
      font-weight: bold;
      color: #a4a5a9;
    }
    .time {
      position: absolute;
      top: 66.2vh;
      font-size: 32rpx;
      font-weight: bold;
      padding-right: 8rpx;
      background-color: #f9f7f8;
    }
    .collection-time {
      left: 9.2vw;
    }
    .result-time {
      left: 54vw;
    }
  }
</style>
