<template>
	<section>
		<button @click="goBack" class="mb-2 text-sm text-gray-500 hover:underline">← Quay lại</button>
		<h1 class="mb-4 text-xl font-semibold">Lịch sử đơn hàng</h1>
		<ul class="space-y-3">
			<li v-for="o in orders" :key="o.id" class="rounded-lg border p-4 dark:border-gray-800">
				<div class="flex items-center justify-between">
					<div>
						<p class="font-medium">Đơn #{{ o.id }}</p>
						<p class="text-sm text-gray-500">Ngày {{ o.date }} · {{ o.status }}</p>
					</div>
					<div class="text-right">
						<p class="font-semibold">{{ formatCurrency(o.total) }}</p>
						<RouterLink :to="`/orders/${o.id}`" class="text-sm underline">Chi tiết</RouterLink>
					</div>
				</div>
			</li>
		</ul>
	</section>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';
import { formatCurrency } from '../utils/helpers';

const orders = ref([]);
const router = useRouter();
onMounted(() => {
	// Demo data - replace with API call when backend is ready
	orders.value = [
		{ id: 101, date: '2025-11-11', status: 'Delivered', total: 1250000 },
		{ id: 102, date: '2025-11-10', status: 'Processing', total: 560000 },
		{ id: 103, date: '2025-11-09', status: 'Shipped', total: 890000 }
	];
});
function goBack() {
	router.back();
}
</script>


