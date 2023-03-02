<template>
  <view>
    <!-- 轮播图的区域，swp生成 -->
<!--    <swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" :circular="true">
      <swiper-item v-for="(item, i) in swiperList" :key="i">
          <image :src="item.image_src"></image>
      </swiper-item>
    </swiper> -->
	<my-search @click="gotoSearch()"></my-search>
	
  </view>
</template>

<script>
  export default {
    data() {
      return {
        swiperList: [],
        foodList: []
      };
    },
    onLoad() {
      // this.getSwiperList()
      // this.getFoodList()
    },
    methods: {
      async getSwiperList() {
        const {data: res} = await uni.$http.get('/home/swiperdata')
        if (res.status !== 200)
          return uni.$showMsg()
        this.swiperList = res.message
      },
      async getFoodList() {
        const {data: res} = await uni.$http.get('/detail')
        if (res.status !== 200)
          return uni.$showMsg()
        this.foodList = res.message
        console.log(this.foodList);
      },
	  gotoSearch() {
		  uni.navigateTo({
		  	url: "/subpkg/search/search"
		  })
	  }
    }
  }
</script>

<style lang="scss">

</style>
