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
					<div class="ui red inverted segment" v-if="errorMsg">
						{{ errorMsg }}
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
				errorMsg: '',
				isCreating: false
			};
		},
		methods: {
			openForm(){
				this.isCreating = true;
			},
			closeForm(){
				this.errorMsg = '';
				this.isCreating = false;
			},
			sendForm(){
				if(this.titleText.length == 0) {
					this.errorMsg = 'Введите название проекта'
					return
				}
				if(this.projectText.length == 0) {
					this.errorMsg = 'Введите описание проекта'
					return
				}
				const title = this.titleText;
				const project = this.projectText;
				this.$emit('create-todo', {
					title,
					project,
					done: false
				});
				this.titleText = '';
				this.projectText = '';
				this.errorMsg = '';
				this.isCreating = false;
			}
		}
	}
</script>
<style></style>