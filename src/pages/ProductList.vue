<template>
	<section>
		<h1 class="mb-4 text-xl font-semibold">Danh sách sản phẩm</h1>
		<div class="grid gap-6 md:grid-cols-[240px_1fr]">
			<aside class="space-y-4">
				<InputField v-model="filters.q" label="Từ khóa" placeholder="Tìm kiếm..." />
				<SelectDropdown v-model="filters.sort" label="Sắp xếp" :options="sortOptions" />
				<InputField v-model="filters.min" label="Giá từ" type="number" />
				<InputField v-model="filters.max" label="Giá đến" type="number" />
				<button class="w-full rounded bg-gray-900 px-3 py-2 text-white dark:bg-gray-100 dark:text-black" @click="applyFilters">
					Lọc
				</button>
			</aside>
			<div>
				<div v-if="loading" class="grid gap-4 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
					<div v-for="i in 8" :key="i" class="h-64 animate-pulse rounded-lg bg-gray-100 dark:bg-gray-800"></div>
				</div>
				<div v-else class="grid gap-4 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
					<ProductCard v-for="p in items" :key="p.id" :product="p" @add="addToCart" />
				</div>
			</div>
		</div>
	</section>
</template>

<script setup>
import { onMounted, reactive, computed } from 'vue';
import { useProductsStore } from '../stores/products';
import { useCartStore } from '../stores/cart';
import InputField from '../components/forms/InputField.vue';
import SelectDropdown from '../components/forms/SelectDropdown.vue';
import ProductCard from '../components/common/ProductCard.vue';
import { formatCurrency } from '../utils/helpers';

const products = useProductsStore();
const cart = useCartStore();
const loading = computed(() => products.loading);
const items = computed(() =>
	products.items.map((p) => ({
		id: p.id,
		name: p.title ?? p.name,
		price: p.price,
		brand: p.brand ?? 'Brand',
		image: p.thumbnail ?? (p.images?.[0] || 'https://picsum.photos/400')
	}))
);

const filters = reactive({ q: '', sort: 'newest', min: '', max: '' });
const sortOptions = [
	{ value: 'newest', label: 'Mới nhất' },
	{ value: 'price_asc', label: 'Giá tăng dần' },
	{ value: 'price_desc', label: 'Giá giảm dần' }
];

onMounted(() => products.fetchList({ limit: 24 }));

function applyFilters() {
	const params = {};
	if (filters.q) params.q = filters.q;
	products.fetchList(params);
}
function addToCart(p) {
	cart.addItem(p, 1);
}
</script>


