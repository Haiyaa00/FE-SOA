<template>
	<h1 class="mb-4 text-xl font-semibold">Quản lý đơn hàng</h1>
	<div class="mb-4 flex gap-3">
		<SelectDropdown v-model="status" :options="statusOptions" />
		<button class="rounded border px-3 py-2 dark:border-gray-700" @click="load">Tải</button>
	</div>
	<div class="overflow-x-auto rounded-lg border dark:border-gray-800">
		<table class="min-w-full text-sm">
			<thead class="bg-gray-50 text-left dark:bg-gray-900">
				<tr>
					<th class="p-3">Mã</th>
					<th class="p-3">Ngày</th>
					<th class="p-3">Khách</th>
					<th class="p-3">Trạng thái</th>
					<th class="p-3">Hành động</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="o in orders" :key="o.id" class="border-t dark:border-gray-800">
					<td class="p-3">#{{ o.id }}</td>
					<td class="p-3">{{ o.date }}</td>
					<td class="p-3">{{ o.customer }}</td>
					<td class="p-3">{{ o.status }}</td>
					<td class="p-3">
						<button class="text-emerald-600 underline" @click="update(o, 'Shipped')">Giao hàng</button>
						<button class="ml-3 text-red-600 underline" @click="update(o, 'Cancelled')">Huỷ</button>
					</td>
				</tr>
			</tbody>
		</table>
	</div>
</template>

<script setup>
import { ref } from 'vue';
import AdminLayout from '../../components/layout/AdminLayout.vue';
import SelectDropdown from '../../components/forms/SelectDropdown.vue';
import { useUIStore } from '../../stores/ui';

const ui = useUIStore();
const status = ref('all');
const statusOptions = [
	{ value: 'all', label: 'Tất cả' },
	{ value: 'Processing', label: 'Đang xử lý' },
	{ value: 'Shipped', label: 'Đã giao' },
	{ value: 'Cancelled', label: 'Đã hủy' }
];
const orders = ref([
	{ id: 401, date: '2025-11-11', customer: 'Nguyễn A', status: 'Processing' },
	{ id: 402, date: '2025-11-10', customer: 'Trần B', status: 'Shipped' }
]);

function load() {
	/* demo filters */
}
function update(o, s) {
	o.status = s;
	ui.pushToast({ type: 'success', message: `Đã cập nhật #${o.id} → ${s}` });
}
</script>


