<template>
	<view class="content">
		<TodoHeader v-if="list.length !== 0" :total="listData.length" :tab="text" :active="activeIndex" @change="tab" />
		<TodoEmpty v-if="list.length === 0" />
		<TodoListItem :source="listData" @finish="finish" />
		<TodoCreate ref="todoCreate" @add="add" />
	</view>
</template>

<script>
	import TodoHeader from './todo-header.vue';
	import TodoListItem from './todo-list-item.vue';
	import TodoCreate from './todo-create.vue';
	import TodoEmpty from './todo-empty.vue';

	export default {
		name: "todo-list",
		components: {
			TodoHeader,
			TodoListItem,
			TodoCreate,
			TodoEmpty
		},
		data() {
			return {
				list: [],
				activeIndex: 0,
				text: '全部',
			}
		},
		onLoad() {},
		computed: {
			listData() {
				let list = JSON.parse(JSON.stringify(this.list));
				let newList = [];

				// 点击 全部 
				if (this.activeIndex === 0) {
					this.text = '全部';
					return list;
				}

				// 点击 待办事项 
				if (this.activeIndex === 1) {
					// checked = false 
					list.forEach((item) => {
						if (!item.checked) {
							newList.push(item);
						}
					});
					this.text = '待办';
					return newList;
				}

				// 点击 已完成 
				if (this.activeIndex === 2) {
					// checked = ture 
					list.forEach((item) => {
						if (item.checked) {
							newList.push(item);
						}
					});
					this.text = '已完成';
					return newList
				}
				return [];
			},
		},
		methods: {
			
			// 发布 
			add(value) {
				if (value === '') {
					uni.showToast({
						title: "请输入内容",
						icon: 'none'
					});
					return;
				}

				this.list.unshift({
					id: 'id' + new Date().getTime(),
					content: value,
					checked: false
				});

				this.close();
			},
			
			close(){
				this.$refs.todoCreate.close();
			},

			// 点击列表触发 
			finish(id) {
				let index = this.list.findIndex((item) => item.id === id);
				console.log('我被点击了', this.list[index]);
				this.list[index].checked = !this.list[index].checked;
			},
			
			tab(index) {
				this.activeIndex = index;
			}
		}
	}
</script>

<style>
</style>