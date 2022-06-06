<template>
	<div id="root">
		<div class="todo-container">
			<div class="todo-wrap">
                <MyTop @add = 'add'></MyTop>
                <MyList :todos = 'todos'></MyList>
                <MyBottom :todos = 'todos'></MyBottom>
			</div>
		</div>
	</div>
</template>

<script>
import MyTop from "./components/MyTop.vue"
import MyList from "./components/MyList.vue"
import MyBottom from "./components/MyBottom.vue"

export default {
    name: 'App',
    components: {
        MyTop,
        MyList,
        MyBottom
    },
	data(){
		return {
			todos:JSON.parse(localStorage.getItem('todos')) || []
		}
	},
	methods:{
		add(things){
			this.todos.unshift(things)
		},
		changeStatus(id){
			this.todos.forEach((things) => {
				if(things.id === id){
					things.completed = !things.completed
				}
			});
		},
		deleteThings(id){
			this.todos.forEach((things) => {
				if(things.id === id) {
					this.todos.splice(this.todos.indexOf(things),1)
				}
			});
		}
	},
	watch: {
			todos:{
				deep:true,
				handler(value){
					localStorage.setItem('todos',JSON.stringify(value))
				}
			}
		},
	mounted() {
		this.$bus.$on('changeStatus',this.changeStatus)
		this.$bus.$on('deleteThings',this.deleteThings)
	},
	beforeDestroy() {
		this.$bus.$off('changeStatus',this.changeStatus)
		this.$bus.$off('deleteThings',this.deleteThings)
	},
}
</script>

<style>
 	body {
		background: #fff;
	}
	.btn {
		display: inline-block;
		padding: 4px 12px;
		margin-bottom: 0;
		font-size: 14px;
		line-height: 20px;
		text-align: center;
		vertical-align: middle;
		cursor: pointer;
		box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
		border-radius: 4px;
	}
	.btn-danger {
		color: #fff;
		background-color: #da4f49;
		border: 1px solid #bd362f;
	}
	.btn-danger:hover {
		color: #fff;
		background-color: #bd362f;
	}
	.btn-edit {
		color: #fff;
		background-color: #5929dc;
		border: 1px solid #1d0560;
		margin-right: 3px;
	}
	.btn-edit:hover {
		color: #fff;
		background-color: #1d0560;
	}
	.btn:focus {
		outline: none;
	}
	.todo-container {
		width: 600px;
		margin: 0 auto;
	}
	.todo-container .todo-wrap {
		padding: 10px;
		border: 1px solid #ddd;
		border-radius: 5px;
	} 
</style>