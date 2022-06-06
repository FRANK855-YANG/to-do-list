<template>
	<div class="todo-footer" v-show="todos.length">
		<label>
			<input type="checkbox" :checked="allFinished">
		</label>
		<span>
			<span>{{finishedThings}}  /  {{todos.length}}  已完成</span>
		</span>
		<button class="btn btn-danger">清除已完成任务</button>
	</div>
</template>

<script>
export default {
    name:'MyBottom',
	props:['todos'],
	computed:{
		finishedThings(){
            let n = 0
		    this.todos.forEach((things) => {
				if(things.completed === true){
					n++
				}
			});
			return n 
		},
		allFinished(){
			let n = 0
		    this.todos.forEach((things) => {
				if(things.completed === true){
					n++
				}
			});
			return n === this.todos.length && this.todos.length > 0 ? true : false
		}
	}
}
</script>

<style>
	/*footer*/
	.todo-footer {
		height: 40px;
		line-height: 40px;
		padding-left: 6px;
		margin-top: 5px;
	}

	.todo-footer label {
		display: inline-block;
		margin-right: 20px;
		cursor: pointer;
	}

	.todo-footer label input {
		position: relative;
		top: -1px;
		vertical-align: middle;
		margin-right: 5px;
	}

	.todo-footer button {
		float: right;
		margin-top: 5px;
	}
</style>