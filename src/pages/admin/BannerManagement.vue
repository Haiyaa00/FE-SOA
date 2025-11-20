<template>
	<h1 class="mb-4 text-xl font-semibold">Quản lý banner</h1>
	<div class="grid gap-4 sm:grid-cols-2 lg:grid-cols-3">
		<div v-for="b in banners" :key="b.id" class="rounded-lg border p-3 dark:border-gray-800">
			<img :src="b.image" class="aspect-[3/1] w-full rounded object-cover" />
			<div class="mt-2 flex justify-between text-sm">
				<span>{{ b.title }}</span>
				<button class="text-red-600 underline" @click="remove(b.id)">Xóa</button>
			</div>
		</div>
	</div>
	<button class="mt-4 rounded bg-gray-900 px-3 py-2 text-white dark:bg-gray-100 dark:text-black" @click="add">Thêm banner</button>
</template>

<script setup>
import { ref } from 'vue';
import AdminLayout from '../../components/layout/AdminLayout.vue';
import { useUIStore } from '../../stores/ui';
const ui = useUIStore();
const banners = ref([
	{ id: 1, title: 'Sale 11.11', image: 'https://picsum.photos/1200/400?1' },
	{ id: 2, title: 'Xmas', image: 'https://picsum.photos/1200/400?2' }
]);
function add() {
	banners.value.unshift({ id: crypto.randomUUID(), title: 'New', image: 'https://picsum.photos/1200/400?random' });
	ui.pushToast({ type: 'success', message: 'Đã thêm banner' });
}
function remove(id) {
	banners.value = banners.value.filter((b) => b.id !== id);
	ui.pushToast({ type: 'success', message: 'Đã xóa banner' });
}
</script>


