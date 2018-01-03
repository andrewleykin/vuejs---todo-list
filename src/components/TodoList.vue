<template>
	<div>
		<p class="tasks">Выполненые задачи: {{todos.filter(todo => {return todo.done === true}).length}} </p>
		<p class="tasks">В работе: {{todos.filter(todo => {return todo.done === false}).length}}</p>
		<todo 
			@delete-todo="deleteTodo"
			@complete-todo="completeTodo"
			@working-todo="workingTodo"
			v-for="todo in todos" 
			:todo.sync="todo"
		></todo>
	</div>
</template>

<script>
	import sweetalert from 'sweetalert';
	import Todo from './Todo.vue';

	export default {
		props: ['todos'],
		components: {
			Todo
		},
		methods: {
			deleteTodo(todo) {
				sweetalert({
					title: 'Ты серьезно?',
					text: 'Эта задача будет удалена!',
					icon: 'warning',
					buttons: ["Нет!", "Удалить!"],
					dangerMode: true
				})
				.then((willDelete) => {
					if (willDelete) {
					const todoIndex = this.todos.indexOf(todo);
					this.todos.splice(todoIndex, 1);
					sweetalert('Удалено!', 'Твоя задача удалена', 'success');
					}
				});
			},
			completeTodo(todo) {
				const todoIndex = this.todos.indexOf(todo);
				this.todos[todoIndex].done = true;
				sweetalert('Успех!', 'Задача выполнена!', 'success');
			},
			workingTodo(todo) {
				const todoIndex = this.todos.indexOf(todo);
				this.todos[todoIndex].done = false;
				sweetalert('Оу!', 'Надо поработать!', 'error');
			}
		}
	};
</script>

<style scoped>
	.tasks {
		text-align: center;
	}
</style>