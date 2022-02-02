<script lang="ts" setup>
	import { computed, reactive } from 'vue'
	import Box from './ui/Box.vue'
	import Button from './ui/Button.vue'
	import Input from './ui/Input.vue'
	import Label from './ui/Label.vue'
	import { FormData } from '../types/data'

	const data = reactive({} as FormData)

	const sendForm = () => {
		console.log(data)
	}
</script>

<template>
	<main class="flex flex-col justify-center items-center h-full bg-gray-700">
		<form class="container relative w-80" @submit.prevent="sendForm">
			<div
				class="absolute -right-4 -bottom-4 h-full w-full bg-purple-600 rounded-xl shadow-2xl"
			></div>

			<div class="relative bg-gray-200 p-7 rounded-xl shadow-2xl">
				<h1 class="text-2xl mb-2 text-purple-600">Formulário</h1>

				<Box>
					<Label for="name" msg="Nome completo:" />
					<Input type="text" id="name" v-model="data.fullName" />
				</Box>

				<Box>
					<Label for="birth" msg="Data de nascimento:" />
					<Input type="date" id="birth" v-model="data.birthday" />
				</Box>

				<Box>
					<Label for="age" msg="Idade:" />
					<Input type="number" id="age" v-model="data.age" />
				</Box>

				<Box>
					<Label for="email" msg="E-mail:" />
					<Input type="email" id="email" v-model="data.email" />
				</Box>

				<Box>
					<Label for="phone" msg="Telefone:" />
					<Input type="number" id="text" v-model="data.phone" />
				</Box>

				<Box>
					<select id="document">
						<option hidden>Selecione:</option>
						<option value="cnh">CNH</option>
						<option value="cpf">CPF</option>
						<option value="rg">RG</option>
					</select>
				</Box>

				<Box>
					<Input type="number" id="document" v-model="data.document" />
				</Box>

				<Button />
			</div>
		</form>
	</main>
</template>
