<template>
	<view>
		<view class="food-img">
			<image :src="food.img" mode="widthFix"></image>
		</view>
		<view class="food-info">
			<uni-list>
				<uni-list-item :title="'名称：' + food.title"></uni-list-item>
				<uni-list-item :title="'生产时间：' + food.prod_time"></uni-list-item>
				<uni-list-item :title="'有效期(天)：' + food.valid_day"></uni-list-item>
				<uni-list-item :title="'类别：' + food.category_title"></uni-list-item>
				<uni-list-item :title="'厨师：' + food.cook_name"></uni-list-item>
			</uni-list>
		</view>

		<view class="ingredient-info">
			<uni-list v-for="(ing, i) in food.ingredients" :key="i">
				<uni-list-item :title="ing.title + '\t' + ing.consumption"></uni-list-item>
			</uni-list>
		</view>

		<view class="food-nav">
			<uni-goods-nav :fill="true" :options="options" :buttonGroup="buttonGroup" @click="onClick"
				@buttonClick="buttonClick" />
		</view>
	
	</view>

	
</template>

<script>
	export default {
		data() {
			return {
				food: {},

				options: [{
					icon: 'headphones',
					text: '客服'
				}, {
					icon: 'shop',
					text: '店铺',
					info: 2,
					infoBackgroundColor: '#007aff',
					infoColor: "red"
				}, {
					icon: 'cart',
					text: '购物车',
					info: 2
				}],
				buttonGroup: [{
						text: '加入购物车',
						backgroundColor: '#ff0000',
						color: '#fff'
					},
					{
						text: '立即购买',
						backgroundColor: '#ffa200',
						color: '#fff'
					}
				]
			};
		},
		onLoad(options) {
			const food_id = options.food_id
			this.getFoodInfo(food_id)
		},
		methods: {
			async getFoodInfo(food_id) {
				const {
					data: res
				} = await uni.$http.get('/food/detail?food_id=' + food_id)
				if (res.status !== 200)
					return uni.$showMsg()
				this.food = res.message
			}
		}
	}
</script>

<style lang="scss">
	.food-img {
		image {
			width: 100%;
		}
	}

	.food-info {
		padding-bottom: 20px;
	}
</style>
