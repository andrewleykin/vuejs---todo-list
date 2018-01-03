<template>
	<div class="ui basic content center aligned segment">
		<button class="ui basic button icon" @click="openForm" v-show="!isCreating">
			<i class="plus icon"></i>
		</button>
		<div class='ui centered card' v-show="isCreating">
			<div class='content'>
				<div class='ui form'>
					<div class='field'>
						<label>Заголовок</label>
						<input type='text' v-model="titleText">
					</div>
					<div class='field'>
						<label>Проект</label>
						<input type='text' v-model="projectText">
					</div>
					<div class='ui two attached'>
						<button class='ui basic blue button' @click="sendForm()">Создать</button>
						<button class='ui basic red button' @click="closeForm">Закрыть</button>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>
<script>
	export default {
		data() {
			return {
				titleText: '',
				projectText: '',
				isCreating: false
			};
		},
		methods: {
			openForm(){
				this.isCreating = true;
			},
			closeForm(){
				this.isCreating = false;
			},
			sendForm(){
				if (this.titleText.length > 0 && this.projectText.length > 0) {
					const title = this.titleText;
					const project = this.projectText;
					this.$emit('create-todo', {
						title,
						project,
						done: false
					});
					this.titleText = '';
					this.projectText = '';
					this.isCreating = false;
				}
				this.isCreating = false;
			}
		}
	}
</script>
<style></style>