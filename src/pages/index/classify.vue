<template>
  <div class="classify-container"
       :class="{'positionFixed':navFixed}">
    <div class="scroll-wrap">
      <div v-if="!isRotate"
           class="classify-items">
        <scroll-view scroll-x
                     :scroll-left='currentIndex*50'
                     style="width: 100%">
          <span v-for="(item,i) in classfies"
                @click="currentIndex=i"
                :class="{isChoose:currentIndex === i}"
                :key="item">
            {{item}}
          </span>
        </scroll-view>
      </div>
      <div v-else
           class="classify-items">
        <span class="all-word">全部分类</span>
      </div>
      <div class="classify-img"
           :class="{rotate:isRotate}"
           @click="isRotate=!isRotate">
        <img src="/static/images/arrow.png">
      </div>
    </div>
    <div class="all-classify"
         @click="isRotate=false"
         catchtouchmove="preventdefault"
         :class="{grow:isRotate}">
      <div class="classify-details"
           @click.stop>
        <span v-for="(item,i) in classfies"
              @click.stop="currentIndex=i"
              :class="{choose:currentIndex === i}"
              :key="i">{{item}}</span>
        <span v-if="classfies.length%4===3"
              style="visibility:hidden"></span>
        <span v-if="classfies.length%4===2"
              style="visibility:hidden"></span>
        <span v-if="classfies.length%4===2"
              style="visibility:hidden"></span>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props:['navFixed'],
  data() {
    return {
      classfies: [],
      isRotate: false,
      currentIndex: 0
    }
  },
  onLoad() {
    this.classfies = ['小猪佩奇', '超级肥效', '奥特曼', '变形金刚', '幽游白书', '超人', '我的路', '火影忍者', '一拳超人', '海贼王']
  }
}
</script>
<style lang="less" scoped>
.positionFixed {
  position: fixed !important;
  top: 0;
  left: 0;
}
.classify-container {
  width: 100%;
  font-size: 28rpx;
  position: relative;
  box-sizing: border-box;
  padding-bottom: 30rpx;
  background-color: #fff;
  z-index: 99;
  .scroll-wrap {
    width: 100%;
    display: flex;
    align-items: center;
    flex-shrink: 0;
    .classify-items {
      padding: 0 20rpx;
      height: 80rpx;
      line-height: 80rpx;
      flex: 1;
      white-space: nowrap;
      overflow: hidden;
      box-sizing: border-box;
      span {
        display: inline-block;
        height: 80rpx;
        margin: 0 10rpx;
        box-sizing: border-box;
        border-bottom: 10rpx solid transparent;
        &.all-word {
          font-size: 30rpx;
        }
      }
      .isChoose {
        border-bottom: 10rpx solid rgb(197, 25, 146);
      }
    }
    .classify-img {
      width: 100rpx;
      display: flex;
      justify-content: center;
      border-left: 2rpx solid #999;
      img {
        transition: 0.5s all;
        width: 50rpx;
        height: 50rpx;
      }
      &.rotate {
        img {
          transform: rotate(-180deg);
        }
      }
    }
  }
  .all-classify {
    width: 100%;
    height: 0;
    overflow: hidden;
    position: absolute;
    left: 0;
    top: 100%;
    background-color: rgba(95, 88, 88, 0.562);
    transition: 0.5s all;
    &.grow {
      height: 100vh;
    }
    .classify-details {
      background-color: #fff;
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap;
      padding: 0 20rpx;
      span {
        width: 150rpx;
        box-sizing: border-box;
        padding: 10rpx;
        text-align: center;
        border: 2rpx solid #999;
        margin-bottom: 30rpx;
      }
      .choose {
        border: 2rpx solid red;
        color: red;
      }
    }
  }
}
::-webkit-scrollbar {
  width: 0;
  height: 0;
  color: transparent;
}
</style>

