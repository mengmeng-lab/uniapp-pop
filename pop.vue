<template>
	<view>
		<button type="default" @click="show">点击弹出框</button>
		<switchEdit :direction="direction" @close="Close" :Uptag="Uptag" :bodyBtn="true">
			<!-- 插槽 -->
			<view class="sitch-box" v-show="Uptag==true">
				<view class="top">
					
				</view>
				<view class="bottom">
					
				</view>
			</view>
		</switchEdit>
	</view>
</template>

<script>
	import switchEdit from '@/components/switch/switch.vue'
	export default {
		components: {
			switchEdit
		},
		data() {
			return {
			//必写
				//弹出方向
				direction: 'bottom',
				//弹出标志
				Uptag: false
			}
		},
		methods: {
			//打开弹框
			show() {
				this.Uptag = !this.Uptag
			},
			//关闭按钮
			Close(data) {
				this.Uptag = data
			}
		}
	}
</script>

<style>
	button {
		width: 300rpx;
		height: 60rpx;
		line-height: 60rpx;
		font-size: 30rpx;
	}
	.sitch-box {
		/* 为了控制位置 */
		position: absolute;
		top: 200rpx;
		left: 50%;
		margin-left: -250rpx;
		width: 500rpx;
		height: 200rpx;
		background-color: #FFFFFF;
		border-radius: 20rpx;
		/* ,其中最主要的功能是层叠顺序 */
		z-index: 999;
	}
	.top,
	.bottom {
		width: 100%;
		height: 100rpx;
	}
	.top {
		border-bottom: 1rpx solid #1B2126;
	}
</style>

