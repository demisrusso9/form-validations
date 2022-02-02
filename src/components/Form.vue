<script lang="ts" setup>
	import { computed, reactive } from 'vue'
	import useValidate from '@vuelidate/core'
	import { required, email, minLength, helpers, maxValue } from '@vuelidate/validators'
	import Box from './ui/Box.vue'
	import Button from './ui/Button.vue'
	import Input from './ui/Input.vue'
	import Label from './ui/Label.vue'
	import { FormData } from '../types/data'
	import Error from './ui/Error.vue'

	const data = reactive({} as FormData)

	const rules = computed(() => {
		return {
			fullName: {
				required: helpers.withMessage('Preencha seu nome', required),
				minLength: helpers.withMessage('Tem que ter no mínimo 4 caracteres', minLength(4))
			},
			birthday: {
				required: helpers.withMessage('Preencha sua data de nascimento', required)
			},
			age: {
				required: helpers.withMessage('Preencha sua idade', required),
				minLength: helpers.withMessage(`Você tem mesmo essa idade? `, maxValue(130))
			},
			email: {
				required: helpers.withMessage('Preencha seu e-mail', required),
				email: helpers.withMessage('E-mail inválido', email)
			},
			phone: {
				required: helpers.withMessage('Preencha seu número de telefone', required)
			}
		}
	})

	const v$ = useValidate(rules, data)

	const sendForm = () => {
		v$.value.$validate()
		console.log(v$.value.$error)

		if (!v$.value.$error) alert('Formulário enviado para nenhum lugar :)')
	}
</script>

<template>
	<main class="flex flex-col justify-center items-center h-full p-2 bg-gray-700">
		<form class="container relative w-80" @submit.prevent="sendForm">
			<div
				class="absolute -right-4 -bottom-4 h-full w-full bg-purple-600 rounded-xl shadow-2xl"
			></div>

			<div class="relative bg-gray-200 px-5 py-6 rounded-xl shadow-2xl">
				<h1 class="text-2xl mb-2 text-purple-600">Formulário</h1>

				<Box>
					<Label for="name" msg="Nome completo:" />
					<Input type="text" id="name" v-model="data.fullName" />
					<Error v-if="v$.fullName.$error">{{ v$.fullName.$errors[0].$message }}</Error>
				</Box>

				<Box>
					<Label for="birth" msg="Data de nascimento:" />
					<Input type="date" id="birth" v-model="data.birthday" />
					<Error v-if="v$.fullName.$error">{{ v$.birthday.$errors[0].$message }}</Error>
				</Box>

				<Box>
					<Label for="age" msg="Idade:" />
					<Input type="number" id="age" v-model="data.age" />
					<Error v-if="v$.fullName.$error">{{ v$.age.$errors[0].$message }}</Error>
				</Box>

				<Box>
					<Label for="email" msg="E-mail:" />
					<Input type="text" id="email" v-model="data.email" />
					<Error v-if="v$.fullName.$error">{{ v$.email.$errors[0].$message }}</Error>
				</Box>

				<Box>
					<Label for="phone" msg="Telefone:" />
					<Input type="tel" id="phone" v-model="data.phone" />
					<Error v-if="v$.fullName.$error">{{ v$.phone.$errors[0].$message }}</Error>
				</Box>

				<Button />
			</div>
		</form>
	</main>
</template>
