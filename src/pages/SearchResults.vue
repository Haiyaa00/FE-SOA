<template>
	<section>
		<h1 class="mb-4 text-xl font-semibold">Kết quả tìm kiếm cho "{{ q }}"</h1>
		<div v-if="loading" class="grid gap-4 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
			<div v-for="i in 8" :key="i" class="h-64 animate-pulse rounded-lg bg-gray-100 dark:bg-gray-800"></div>
		</div>
		<div v-else-if="!items.length" class="rounded-lg border p-8 text-center text-sm text-gray-500 dark:border-gray-800">Không tìm thấy sản phẩm</div>
		<div v-else class="grid gap-4 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
			<ProductCard v-for="p in items" :key="p.id" :product="p" @add="addToCart" />
		</div>
	</section>
</template>

<script setup>
import { ref, watchEffect } from 'vue';
import { useRoute } from 'vue-router';
import api from '../utils/api';
import ProductCard from '../components/common/ProductCard.vue';
import { useCartStore } from '../stores/cart';

const route = useRoute();
const cart = useCartStore();
const q = ref('');
const loading = ref(false);
const items = ref([]);

watchEffect(async () => {
	q.value = String(route.query.q || '');
	if (!q.value) {
		items.value = [];
		return;
	}
	loading.value = true;
	try {
		// Dummyjson search
		const { data } = await api.get(`/products/search?q=${encodeURIComponent(q.value)}`);
		items.value = (data.products ?? []).map((p) => ({
			id: p.id,
			name: p.title,
			price: p.price,
			brand: p.brand ?? 'Brand',
			image: p.thumbnail ?? (p.images?.[0] || 'https://picsum.photos/400')
		}));
	} finally {
		loading.value = false;
	}
});

function addToCart(p) {
	cart.addItem(p, 1);
}
</script>


