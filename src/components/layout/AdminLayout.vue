<template>
	<div class="min-h-screen lg:grid lg:grid-cols-[240px_1fr]">
		<aside class="hidden border-r bg-gray-50 p-4 dark:border-gray-800 dark:bg-gray-900 lg:block">
			<h2 class="mb-4 font-semibold">Admin</h2>
			<nav class="flex flex-col gap-2 text-sm">
				<RouterLink to="/admin" class="hover:underline">Dashboard</RouterLink>
				<RouterLink to="/admin/products" class="hover:underline">Products</RouterLink>
				<RouterLink to="/admin/orders" class="hover:underline">Orders</RouterLink>
				<RouterLink to="/admin/users" class="hover:underline">Users</RouterLink>
				<RouterLink to="/admin/banners" class="hover:underline">Banners</RouterLink>
				<RouterLink to="/admin/reports" class="hover:underline">Reports</RouterLink>
			</nav>
		</aside>
		<div>
			<header class="border-b px-4 py-3 flex items-center justify-between dark:border-gray-800">
				<RouterLink to="/" class="text-sm text-gray-500 hover:underline">← Quay lại trang chủ</RouterLink>
				<button @click="logout" class="ml-4 rounded bg-gray-900 px-3 py-1 text-white text-sm dark:bg-gray-100 dark:text-black">Đăng xuất</button>
			</header>
			<main class="px-4 py-6">
				<slot />
			</main>
		</div>
	</div>
</template>

<script setup>
import { useUserStore } from '../../stores/user';
import { useRouter } from 'vue-router';

const user = useUserStore();
const router = useRouter();

function logout() {
	user.logout();
	router.push('/');
}
</script>


