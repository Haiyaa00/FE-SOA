<template>
	<div class="mb-4 flex items-center justify-between">
		<h1 class="text-xl font-semibold">Quản lý sản phẩm</h1>
		<button class="rounded bg-gray-900 px-3 py-2 text-white dark:bg-gray-100 dark:text-black" @click="openCreate">Thêm sản phẩm</button>
	</div>
	<div class="mb-4 grid gap-3 md:grid-cols-3">
		<InputField v-model="filters.q" placeholder="Tìm theo tên..." />
		<SelectDropdown v-model="filters.status" :options="statusOptions" />
		<button class="rounded border px-3 py-2 dark:border-gray-700" @click="load">Lọc</button>
	</div>
	<div class="overflow-x-auto rounded-lg border dark:border-gray-800">
		<table class="min-w-full text-sm">
			<thead class="bg-gray-50 text-left dark:bg-gray-900">
				<tr>
					<th class="p-3">ID</th>
					<th class="p-3">Tên</th>
					<th class="p-3">Giá</th>
					<th class="p-3">Hành động</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="p in items" :key="p.id" class="border-t dark:border-gray-800">
					<td class="p-3">#{{ p.id }}</td>
					<td class="p-3">{{ p.name }}</td>
					<td class="p-3">{{ formatCurrency(p.price) }}</td>
					<td class="p-3">
						<button class="text-emerald-600 underline" @click="edit(p)">Sửa</button>
						<button class="ml-3 text-red-600 underline" @click="remove(p)">Xóa</button>
					</td>
				</tr>
			</tbody>
		</table>
	</div>
</template>

<script setup>
import { ref, onMounted, reactive } from 'vue';
import AdminLayout from '../../components/layout/AdminLayout.vue';
import InputField from '../../components/forms/InputField.vue';
import SelectDropdown from '../../components/forms/SelectDropdown.vue';
import { formatCurrency } from '../../utils/helpers';
import api from '../../utils/api';
import { useUIStore } from '../../stores/ui';

const ui = useUIStore();
const items = ref([]);
const filters = reactive({ q: '', status: 'all' });
const statusOptions = [
	{ value: 'all', label: 'Tất cả' },
	{ value: 'active', label: 'Đang bán' },
	{ value: 'inactive', label: 'Tạm ẩn' }
];

async function load() {
	const { data } = await api.get('/products?limit=20');
	items.value = (data.products ?? data ?? []).map((p) => ({
		id: p.id,
		name: p.title ?? p.name,
		price: p.price
	}));
}
function openCreate() {
	ui.pushToast({ type: 'info', message: 'Màn hình tạo sản phẩm (demo)' });
}
function edit(p) {
	ui.pushToast({ type: 'info', message: `Sửa #${p.id} (demo)` });
}
function remove(p) {
	ui.pushToast({ type: 'success', message: `Đã xóa #${p.id} (demo)` });
	items.value = items.value.filter((i) => i.id !== p.id);
}

onMounted(load);
</script>


