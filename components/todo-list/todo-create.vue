<template>
	<!-- 创建按钮 -->
	<view class="create-todo" @click="create">
		<text class="iconfont icon-jia" :class="{'create-todo-active':textShow}"></text>
	</view>

	<!-- 输入框 -->
	<view v-if="active" class="create-content" :class="{'create--show':textShow}">
		<view class="create-content-box">
			<!-- input 输入 -->
			<view class="create-input">
				<input @focus="()=>{this.plc=''}" @blur="()=>{this.plc='请输入您要创建的任务描述';}" type="text" v-model="value"
					:placeholder="plc" />
				<!-- <uni-easyinput :inputBorder="false" v-model="value" placeholder="请输入您要创建的任务描述"></uni-easyinput> -->
			</view>
			<!-- 发布按钮 -->
			<view class="create-button" @click="handleAdd"> 创建 </view>
		</view>
	</view>
</template>

<script>
	export default {
		emits: ['add'],
		data() {
			return {
				active: false,
				textShow: false,
				value: '',
				plc: '请输入您要创建的任务描述'
			}
		},
		methods: {
			handleAdd() {
				this.$emit('add', this.value)
			},

			// 打开输入框
			create() {
				if (this.active) {
					this.close();
				} else {
					this.open();
				}
			},

			// 打开 动画 
			open() {
				this.active = true;
				this.$nextTick(() => {
					setTimeout(() => {
						this.textShow = true;
					}, 50);
				});
			},

			// 关闭动画
			close() {
				this.value = '';
				this.textShow = false;
				this.$nextTick(() => {
					setTimeout(() => {
						this.active = false
					}, 350);
				});
			},
		}
	}
</script>

<style>
	@import '../../common/icon.css';

	.create-todo {
		display: flex;
		justify-content: center;
		align-items: center;
		position: fixed;
		bottom: 20px;
		left: 0;
		right: 0;
		margin: 0 auto;
		width: 50px;
		height: 50px;
		border-radius: 50%;
		background-color: #deeff5;
		box-shadow: 1px 1px 5px 2px rgba(0, 0, 0, 0.1);
	}

	.icon-jia {
		font-size: 30px;
		color: #add8e6;
	}

	.create-content {
		position: fixed;
		bottom: 95px;
		left: 20px;
		right: 20px;
		transition: all 0.3s;
		opacity: 0;
		transform: scale(0) translateY(200%)
	}

	.create--show {
		opacity: 1;
		transform: scale(1) translateY(0);
	}

	.create-content-box {
		display: flex;
		align-items: center;
		padding: 0 15px;
		padding-right: 0;
		border-radius: 50px;
		background: #DEEFF5;
		box-shadow: 1px 1px 5px 2px rgba(0, 0, 0, 0.1);
		z-index: 2;
	}

	.create-input {
		width: 100%;
		padding-right: 15px;
		color: #add8e6;
	}

	.create-button {
		display: flex;
		justify-content: center;
		align-items: center;
		flex-shrink: 0;
		width: 80px;
		height: 50px;
		border-radius: 50px;
		font-size: 16px;
		color: #88d4ec;
		box-shadow: -2px 0px 2px 1px rgba(0, 0, 0, 0.1);
	}

	.create-content:after {
		content: '';
		position: absolute;
		right: 0;
		left: 0;
		bottom: -8px;
		margin: 0 auto;
		width: 20px;
		height: 20px;
		background: #DEEFF5;
		transform: rotate(45deg);
		box-shadow: 1px 1px 5px 2px rgba(0, 0, 0, 0.1);
		z-index: -1;
	}

	.create-content-box:after {
		content: '';
		position: absolute;
		right: 0;
		left: 0;
		bottom: -8px;
		margin: 0 auto;
		width: 20px;
		height: 20px;
		background: #DEEFF5;
		transform: rotate(45deg);
	}
</style>