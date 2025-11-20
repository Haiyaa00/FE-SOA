<template>
	<h1 class="mb-4 text-xl font-semibold">Quản lý người dùng</h1>
	<div class="overflow-x-auto rounded-lg border dark:border-gray-800">
		<table class="min-w-full text-sm">
			<thead class="bg-gray-50 text-left dark:bg-gray-900">
				<tr>
					<th class="p-3">ID</th>
					<th class="p-3">Tên</th>
					<th class="p-3">Email</th>
					<th class="p-3">Vai trò</th>
					<th class="p-3">Hành động</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="u in users" :key="u.id" class="border-t dark:border-gray-800">
					<td class="p-3">#{{ u.id }}</td>
					<td class="p-3">{{ u.name }}</td>
					<td class="p-3">{{ u.email }}</td>
					<td class="p-3">{{ u.role }}</td>
					<td class="p-3">
						<button class="text-emerald-600 underline" @click="promote(u)">Thăng cấp</button>
						<button class="ml-3 text-red-600 underline" @click="ban(u)">Cấm</button>
					</td>
				</tr>
			</tbody>
		</table>
	</div>
</template>

<script setup>
import { ref } from 'vue';
import AdminLayout from '../../components/layout/AdminLayout.vue';
import { useUIStore } from '../../stores/ui';
const ui = useUIStore();
const users = ref([
	{ id: 1, name: 'Demo Admin', email: 'admin@example.com', role: 'admin' },
	{ id: 2, name: 'Demo User', email: 'user@example.com', role: 'user' }
]);
function promote(u) {
	u.role = 'admin';
	ui.pushToast({ type: 'success', message: `Đã thăng cấp ${u.name}` });
}
function ban(u) {
	ui.pushToast({ type: 'success', message: `Đã cấm ${u.name}` });
}
</script>


