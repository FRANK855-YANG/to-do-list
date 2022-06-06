<template>
	<li>
		<label>
			<input type="checkbox" :checked="things.completed" @click="changeItem(things.id)"/>
			<span>{{things.title}}</span>
		</label>
		<div>
			<button class="btn btn-edit">编辑</button>
		    <button class="btn btn-danger" @click = "deleteItem(things.id)">删除</button>
		</div>
	</li>
</template>

<script>
	export default {
		name:'MyItem',
		props:['things'],
		methods:{
			changeItem(id){
				this.$bus.$emit('changeStatus',id)
			},
			deleteItem(id){
				this.$bus.$emit('deleteThings',id)
			}
		}
	}
</script>

<style scoped>
	/*item*/
	li {
		list-style: none;
		height: 36px;
		line-height: 36px;
		padding: 0 5px;
		border-bottom: 1px solid #ddd;
	}

	li label {
		float: left;
		cursor: pointer;
		}
    li input {
		margin-right: 6px;
		position: relative;
		top: -1px;
	}
	li span {
		margin-right: 6px;
		position: relative;
		top: -3.5px;
	}
    li div {
		display: flex;
		flex-direction: row;
		justify-content: flex-end;
	}
	li button {
		margin-top: 3px;
	}

	li:before {
		content: initial;
	}

	li:last-child {
		border-bottom: none;
	}

	li:hover{
		background-color: #ddd;
	}
	
	li:hover button{
		display: block;
	}
</style>