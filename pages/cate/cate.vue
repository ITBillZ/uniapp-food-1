<template>
	<view>
		<!-- 使用自定义的搜索组件 -->
		<my-search @click="gotoSearch"></my-search>
			<view class="cate-list" v-for="(item, i1) in cateList" :key="i1">
				<!-- 一级列表 -->
				<uni-section :title="item.cate_1" type="line" padding>
					<uni-grid :column="4" :highlight="true">
						<uni-grid-item v-for="(cate_2, i2) in item.cate_2_list" :key="i2">
							<text>{{cate_2}}</text>
						</uni-grid-item>
					</uni-grid>
					
				</uni-section>
			</view>
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
			gotoGoodsList(item) {
				uni.navigateTo({
					url: '/subpkg/goods_list/goods_list?cid=' + item.cat_id
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
	.scroll-view-container {
		display: flex;
		flex-shrink: 0;

		.left-scroll-view {
			width: 100px;

			.left-scroll-view-item {
				background-color: #F7F7F7;
				line-height: 50px;
				text-align: center;
				font-size: 12px;

				// &同时包含两个类名
				&.active {
					background-color: #FFFFFF;
					position: relative;

					&::before {
						content: ' ';
						display: block;
						width: 3px;
						height: 30px;
						background-color: #C00000;
						position: absolute;
						top: 25%;
						left: 0;
						// transform: translateY(-50%);
					}
				}
			}
		}
		
		.right-scroll-view {
			flex-shrink: 0;
		}
	}

	// .right-scroll-view {
	// 	.cate-2-list {
	// 		display: flex;
	// 		flex-wrap: wrap;

	// 		.cate-2-item {
	// 			width: 40%;
	// 			display: flex;
	// 			flex-direction: column;
	// 			justify-content: center;
	// 			align-items: center;
	// 			padding: 5px 5px;
	// 			// margin-bottom: 10px;
	// 			border: 1px solid #cfcfcf;
	// 			text {
	// 				font-size: 18px;
	// 			}
	// 		}
	// 	}
	// }
</style>
