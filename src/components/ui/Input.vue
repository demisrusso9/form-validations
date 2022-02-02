<script lang="ts" setup>
	import { ref, reactive } from 'vue'
</script>

<template>
	<input
		class="rounded-t-md shadow-sm outline-none border-b-2 focus:border-purple-600 transition-colors px-1 text-sm p-1"
		@input="$emit('update:modelValue', ($event.target as HTMLInputElement).value)"
	/>
</template>
