<script lang="ts" setup>
	import { defineProps } from 'vue'

	defineProps<{
		msg: string
	}>()
</script>

<template>
	<label class="mb-1 text-md font-thin select-none">{{ msg }}</label>
</template>
