<template>
	<form @submit.prevent="submit" class="relative">
		<input
			v-model="q"
			type="search"
			placeholder="Tìm kiếm sản phẩm..."
			class="w-full rounded-md border-gray-300 pl-10 shadow-sm focus:border-gray-900 focus:ring-gray-900 dark:border-gray-700 dark:bg-gray-900 dark:text-gray-100"
		/>
		<span class="pointer-events-none absolute left-3 top-1/2 -translate-y-1/2 text-gray-400">🔎</span>
	</form>
</template>

<script setup>
import { ref } from 'vue';
const q = ref('');
const emit = defineEmits(['search']);
function submit() {
	if (!q.value?.trim()) return;
	emit('search', q.value.trim());
}
</script>


