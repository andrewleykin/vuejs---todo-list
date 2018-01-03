<template>
	<div class="ui centered card">
		<div class="content" v-show="!isEditing">
			<div class="header">{{todo.title}}</div>
			<div class="meta">{{todo.project}}</div>
			<div class="extra content">
				<span class="right floated edit icon" @click="showFrom">
					<i class="edit icon"></i>
				</span>
				<span class="right floated trash icon" @click="deleteTodo(todo)">
					<i class="trash icon"></i>
				</span>
			</div>
		</div>
		<div class="content" v-show="isEditing">
			<div class="ui form">
				<div class="field">
					<label>Заголовок</label>
					<input type="text" v-model="todo.title">
				</div>
				<div class="field">
					<label>Проект</label>
					<input type="text" v-model="todo.project">
				</div>
				<div class="ui two button attached buttons">
					<button class="ui basic blue button" @click="hideForm">Close X</button>
				</div>
			</div>
		</div>
		<div 
			class="ui bottom attached green basic button" 
			v-show="!isEditing && todo.done"
			@click="workingTodo(todo)"
		>Завершено</div>
		<div 
			class="ui bottom attached red basic button" 
			v-show="!isEditing && !todo.done" 
			@click="completeTodo(todo)"
		>В работе</div>
	</div>
</template>
<script>
	export default {
		props: ['todo'],
		data () {
			return {
				isEditing: false
			}
		},
		methods: {
			showFrom(){
				this.isEditing = true;
			},
			hideForm(){
				this.isEditing = false;
			},
			deleteTodo(todo) {
				this.$emit('delete-todo', todo);
			},
			completeTodo(todo) {
				this.$emit('complete-todo', todo);
			},
			workingTodo(todo) {
				this.$emit('working-todo', todo);
			}
		}
	};
</script>
<style scoped>
	span.icon {
		cursor: pointer;
	}
</style>