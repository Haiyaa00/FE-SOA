<template>
	<section>
		<button @click="goBack" class="mb-2 text-sm text-gray-500 hover:underline">← Quay lại</button>
		<h1 class="mb-4 text-xl font-semibold">Yêu thích</h1>
		<div class="rounded-lg border p-8 text-center text-sm text-gray-500 dark:border-gray-800">Tính năng demo. Lưu localStorage hoặc gọi API (tùy chọn).</div>
	</section>
</template>

<script setup>
import { useRouter } from 'vue-router';
const router = useRouter();
function goBack() {
	router.back();
}
</script>


