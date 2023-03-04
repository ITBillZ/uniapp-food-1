<template>
	<view>
		<!-- 使用自定义的搜索组件 -->
		<my-search @click="gotoSearch"></my-search>
		<view class="cate-list" v-for="(item, i1) in cateList" :key="i1">
			<!-- 一级列表 -->
			<uni-section :title="item.cate_1" type="line" padding titleFontSize="18px">
				<uni-grid :column="4" :highlight="true">
					<uni-grid-item v-for="(cate_2, i2) in item.cate_2_list" :key="i2">
						<view class="cate-2-item" @click="gotoFoodList(cate_2)">
							<view class="cate-2-img">
								<uni-icons type="shop" :size="40" color="#777"></uni-icons>
							</view>
							<text>{{cate_2}}</text>
						</view>
					</uni-grid-item>
				</uni-grid>

			</uni-section>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 当前设备可用的高度
				wh: 0,
				// 分类列表数据
				cateList: [],
				active: 0,

				scrollTop: 0
			};
		},
		onLoad() {
			// 获取屏幕信息
			const sysInfo = uni.getSystemInfoSync()
			this.wh = sysInfo.windowHeight - 50

			this.getCateList()
		},
		methods: {
			async getCateList() {
				const {
					data: res
				} = await uni.$http.get('/category/list')
				if (res.status !== 200) return uni.$showMsg()
				this.cateList = res.message

			},
			activeChange(i) {
				this.active = i
				// 如果赋的值不变，那么scroll-top不会更改
				this.scrollTop = this.scrollTop === 0 ? 0.1 : 0
			},
			// 跳转到商品列表
			gotoFoodList(cate_2) {
				uni.navigateTo({
					url: '/subpkg/food_list/food_list?cate=' + cate_2
				})
			},
			gotoSearch() {
				uni.navigateTo({
					url: '/subpkg/search/search'
				})
			}
		}

	}
</script>

<style lang="scss">
	.cate-2-item {

		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;

		text {
			text-align: center;
			font-size: 16px;
		}


		.cate-2-img {
			margin-top: 10px;
			display: flex;
			flex-direction: column;
			align-items: center;
		}
	}


	// .scroll-view-container {
	// 	display: flex;

	// 	.left-scroll-view {
	// 		width: 100px;

	// 		.left-scroll-view-item {
	// 			background-color: #F7F7F7;
	// 			line-height: 50px;
	// 			text-align: center;
	// 			font-size: 12px;

	// 			// &同时包含两个类名
	// 			&.active {
	// 				background-color: #FFFFFF;
	// 				position: relative;

	// 				&::before {
	// 					content: ' ';
	// 					display: block;
	// 					width: 3px;
	// 					height: 30px;
	// 					background-color: #C00000;
	// 					position: absolute;
	// 					top: 25%;
	// 					left: 0;
	// 					// transform: translateY(-50%);
	// 				}
	// 			}
	// 		}
	// 	}

	// 	.right-scroll-view {
	// 		flex-shrink: 0;
	// 	}
	// }
</style>
