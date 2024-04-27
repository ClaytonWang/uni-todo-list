<template>
	<!-- 内容 -->
	<view class="todo-content">
		<!-- todo--finish -->
		<view class="todo-list" :class="{'todo--finish':item.checked}" v-for="(item,index) in source" :key="index"
			@click="handleClick(item.id)">
			<view class="todo-list__checkbox">
				<view class="checkbox"></view>
			</view>
			<view class="todo-list__content"> {{item.content}} </view>
		</view>
	</view>
</template>

<script>
	export default {
		emits: ['finish'],
		props: {
			source: {
				type: Array,
				default () {
					return [];
				}
			},
		},
		methods: {
			handleClick(id) {
				this.$emit('finish', id);
			}
		}
	}
</script>

<style>
	.todo-content {
		position: relative;
		padding-top: 50px;
		padding-bottom: 100px;
	}

	.todo-list {
		position: relative;
		display: flex;
		align-items: center;
		padding: 15px;
		margin: 15px;
		color: #0c3854;
		font-size: 14px;
		border-radius: 8px;
		background: #cfebfd;
		box-shadow: 1px 1px 5px 2px rgba(0, 0, 0, 0.1);
		overflow: hidden;
	}

	.todo-list:after {
		position: absolute;
		content: '';
		top: 0;
		bottom: 0;
		left: 0;
		width: 8px;
		background: #91d1e8;
	}

	.todo-list__checkbox {
		padding-right: 15px;
	}

	.checkbox {
		width: 20px;
		height: 20px;
		border-radius: 50%;
		background: #FFFFFF;
		box-shadow: 0 0 5px 1px rgba(0, 0, 0, 0.1);
	}

	.todo--finish .checkbox {
		position: relative;
		background: #eee;
	}

	.todo--finish .checkbox:after {
		content: '';
		position: absolute;
		width: 10px;
		height: 10px;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		margin: auto;
		border-radius: 50%;
		background: #CFEBFD;
		box-shadow: 0 0 2px 0px rgba(0, 0, 0, 0.2);
	}

	.todo--finish .todo-list__content {
		color: #999999;
	}

	.todo--finish.todo-list:before {
		content: '';
		position: absolute;
		top: 0;
		bottom: 0;
		left: 40px;
		right: 10px;
		height: 2px;
		margin: auto 0;
		background: #bdcdd8;
	}

	.todo--finish.todo-list:after {
		background: #cccccc;
	}
</style>