<template>
	<section>
		<div class="mb-6 rounded-xl bg-gradient-to-r from-emerald-500 to-teal-600 p-8 text-white">
			<h1 class="text-2xl font-bold">Khám phá ưu đãi hôm nay</h1>
			<p class="mt-1 text-white/80">Giảm giá đến 50% cho nhiều mặt hàng</p>
		</div>
		<h2 class="mb-3 text-lg font-semibold">Sản phẩm nổi bật</h2>
		<div class="grid gap-4 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
			<ProductCard
				v-for="p in products"
				:key="p.id"
				:product="p"
				@add="addToCart"
				@wishlist="addWishlist"
			/>
		</div>
	</section>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import ProductCard from '../components/common/ProductCard.vue';
import { useCartStore } from '../stores/cart';
import api from '../utils/api';

const cart = useCartStore();
const products = ref([]);

onMounted(async () => {
	// Using dummyjson for demo: https://dummyjson.com/products
	const { data } = await api.get('/products?limit=8');
	products.value = (data.products ?? data ?? []).map((p) => ({
		id: p.id,
		name: p.title ?? p.name,
		price: p.price,
		brand: p.brand ?? 'Brand',
		image: p.thumbnail ?? (p.images?.[0] || 'https://picsum.photos/400')
	}));
});

function addToCart(p) {
	cart.addItem(p, 1);
}
function addWishlist() {
	/* no-op demo */
}
</script>


