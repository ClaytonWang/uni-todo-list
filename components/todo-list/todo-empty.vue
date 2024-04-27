<template>
	<!-- 没有数据的状态 -->
	<view class="default">
		<view class="image-default">
			<image src="../../static/empty.png" mode="aspectFit"></image>
		</view>
		<view class="default-info">
			<view class="default-info__text">您还没有创建任何待办事项</view>
			<view class="default-info__text">点击下方+号创建一个吧</view>
		</view>
	</view>
</template>

<script>
	export default {}
</script>

<style>
	.default {
		padding-top: 100px;
	}

	.image-default {
		display: flex;
		justify-content: center;
	}

	.image-default image {
		width: 100%;
	}

	.default-info {
		text-align: center;
		font-size: 14px;
		color: #CCCCCC;
	}

	.icon-jia {
		transition: transform 0.3s;
	}

	.create-todo-active {
		transform: rotate(135deg);
	}
</style>