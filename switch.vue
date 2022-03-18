<template>
	<view class="box">
		<!-- 组件内关闭 -->
		<button type="default" @click="popBtn()" v-show="bodyBtn == true">底部弹出</button>
		<!--  -->
		<!-- 遮罩层 -->
		<view class="mask" v-show="tag==true || Uptag == true" @click="close()"></view>
		<!-- 插槽 -->
		<slot></slot>
		<!-- 弹窗 -->
		<view class="window-top all-transition" :style="direction=='top' ? objDirection : ''" v-show="direction=='top'">
			顶部弹出
		</view>
		<view class="window all-transition" :style="direction=='bottom' ? objDirection : ''" v-show="direction=='bottom'">
			<view style="text-align: center;font-size: 35rpx;height: 90rpx;border-bottom: 1rpx solid #1B2126;line-height: 90rpx;">
				底部弹出
			</view>
			<button type="default" class="bottom-btn" @tap="close">取消</button>
		</view>
		<view class="window-right all-transition" :style="direction=='right' ? objDirection : ''" v-show="direction=='right'">
			右侧弹出
		</view>
		<view class="window-left all-transition" :style="direction=='left' ? objDirection : ''" v-show="direction=='left'">
			左侧弹出
		</view>
	</view>
</template>

<script>
	// 1.如果先要在组件内部控制显示与隐藏设置bodyBtn为true即可
	// 2.
	export default {
		props: {
			direction: String, //方向
			Uptag: Boolean, //判断点击事件
			bodyBtn: Boolean //组件内容控制显示隐藏
		},
		data() {
			return {
				tag: false //组件内关闭的变量
			}
		},
		computed: {
			//计算函数
			objDirection() {
				if (this.direction == 'bottom') {
					if (this.tag||this.Uptag == true) {
						return "transform: translateY(0);"
					} else {
						return "transform: translateY(100%);"
					}
				} else if (this.direction == 'right') {
					if (this.tag||this.Uptag == true) {
						return "transform: translateX(0);"
					} else {
						return "transform: translateX(100%);"
					}
				} else if (this.direction == 'left') {
					if (this.tag||this.Uptag == true) {
						return "transform: translateX(0);"
					} else {
						return "transform: translateX(-100%);"
					}
				} else if (this.direction == 'top') {
					if (this.tag || this.Uptag == true) {
						return "transform: translateY(0);"
					} else {
						return "transform: translateY(-100%);"
					}
				}
			}
		},
		methods: {
			popBtn() {
				this.tag = !this.tag
			},
			//关闭事件
			close() {
				if (this.tag == true) this.tag = false //组件内关闭事件
				this.$emit('close', false) //组件外关闭事件
			}
		}
	}
</script>

<style>
	.mask {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(0,0,0,0.2);
		z-index: 1;
	}
	.all-transition {
		position: absolute;
		transition: all 0.3s;
		-moz-transition: all 0.3s; /* Firefox 4 */
		-webkit-transition: all 0.3s; /* Safari and Chrome */
		-o-transition: all 0.3s;
		background-color: #FFFFFF;
		z-index: 999;
	}
	.window {
		bottom: 0;
		left: 50%;
		margin-left: -300rpx;
		width: 600rpx;
		height: 500rpx;
		border-radius: 40rpx 40rpx 0 0;
	}
	.window-right {
		/* 如果不想让右侧全屏占满,将top值删掉就可 */
		top: 0;
		right: 0;
		width: 200rpx;
		height: 100%;
		border-radius: 15rpx 0 0 15rpx;
	}
	.window-left {
		/* 如果不想让右侧全屏占满,将top值删掉就可 */
		top: 0;
		left: 0;
		width: 200rpx;
		height: 100%;
		border-radius: 0 15rpx 15rpx 0;
	}
	.window-top {
		left: 50%;
		margin-left: -300rpx;
		/* 如果不想让右侧全屏占满,将top值删掉就可 */
		top: 0;
		width: 600rpx;
		height: 500rpx;
		border-radius: 0 0 15rpx 15rpx;
	}
	.bottom-btn {
		margin-top: 100rpx;
		width: 200rpx;
		height: 80rpx;
		background-color: pink;
	}
</style>

