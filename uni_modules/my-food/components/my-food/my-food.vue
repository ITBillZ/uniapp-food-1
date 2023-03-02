<template>
  <view>
    <view class="food-item">
      <!-- 左侧盒子 -->
      <view class="food-item-left">
        <image :src="food.img" class="food-pic" mode="widthFix"></image>
      </view>
      <!-- 右侧盒子 -->
      <view class="food-item-right">
        <view class="food-name">{{food.title}}</view>
      </view>
    </view>
  </view>
</template>

<script>
  export default {
    name:"my-food",
    props: {
      food: {
        type: Object,
        default: {}
      }
    },
    
    data() {
      return {
        // 默认商品图片
        defaultPic: 'https://img3.doubanio.com/f/movie/8dd0c794499fe925ae2ae89ee30cd225750457b4/pics/movie/celebrity-default-medium.png'
      };
    }
  }
</script>

<style lang="scss">
  .food-item {
    display: flex;
    padding: 10px 5px;
    border-bottom: 1px solid #dfdfdf;
    
    .food-item-left {
      margin-right: 5px;
      .food-pic {
        width: 120px;
        display: block;
      }
    }
    .food-item-right {
      .food-name {
        font-size: 18px;
      }
    }
  }
</style>
