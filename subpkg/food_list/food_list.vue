<template>
  <view>
    <view class="food-list">
      <view v-for="(food, i) in foodList" :key="i"  @click="gotoDetail(food)">
        <my-food :food="food"></my-food>
      </view>
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        foodList: [],
        total: 10
      }
    },
    onLoad() {
      this.getFoodList()
    },
    methods: {
      async getFoodList() {
        const {
          data: res
        } = await uni.$http.get('/food/list')
        if (res.status !== 200)
          return uni.$showMsg()
        this.foodList = res.message
      },
      gotoDetail(food) {
        uni.navigateTo({
          url: "/subpkg/food_detail/food_detail?food_id=" + food.food_id	
        })
      }
    }
  }
</script>

<style lang="scss">

</style>
