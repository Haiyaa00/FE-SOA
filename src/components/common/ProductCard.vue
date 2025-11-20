<template>
	<div class="group rounded-lg border bg-white p-3 shadow-sm transition hover:shadow-md dark:border-gray-800 dark:bg-gray-900">
		<RouterLink :to="`/product/${product.id}`" class="block">
			<img :src="product.image" :alt="product.name" class="aspect-square w-full rounded-md object-cover" />
			<h3 class="mt-3 line-clamp-1 font-medium">{{ product.name }}</h3>
		</RouterLink>
		<p class="mt-1 text-sm text-gray-500">{{ product.brand }}</p>
		<div class="mt-2 flex items-center justify-between">
			<p class="font-semibold">{{ formatCurrency(product.price) }}</p>
			<div class="flex gap-2">
				<button @click="$emit('wishlist', product)" class="rounded border px-2 py-1 text-sm hover:bg-gray-50 dark:border-gray-700 dark:hover:bg-gray-800">♥</button>
				<button @click="$emit('add', product)" class="rounded bg-gray-900 px-3 py-1.5 text-sm text-white hover:bg-black dark:bg-gray-100 dark:text-black">Thêm</button>
			</div>
		</div>
	</div>
</template>

<script setup>
import { formatCurrency } from '../../utils/helpers';
defineProps({
	product: {
		type: Object,
		required: true
	}
});
defineEmits(['add', 'wishlist']);
</script>


