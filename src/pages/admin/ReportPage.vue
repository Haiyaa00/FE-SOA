<template>
	<h1 class="mb-4 text-xl font-semibold">Báo cáo</h1>
	<div class="grid gap-4 md:grid-cols-2">
		<div class="rounded-lg border p-4 dark:border-gray-800">
			<p class="mb-2 font-medium">Doanh thu theo tháng</p>
			<div class="h-48 rounded bg-gray-100 dark:bg-gray-800"></div>
		</div>
		<div class="rounded-lg border p-4 dark:border-gray-800">
			<p class="mb-2 font-medium">Sản phẩm bán chạy</p>
			<div class="h-48 rounded bg-gray-100 dark:bg-gray-800"></div>
		</div>
	</div>
</template>

<script setup>
import AdminLayout from '../../components/layout/AdminLayout.vue';
</script>


