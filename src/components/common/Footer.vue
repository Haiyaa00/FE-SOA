<template>
	<footer class="mt-12 border-t bg-gray-50 py-8 text-sm dark:bg-gray-900">
		<div class="mx-auto max-w-7xl px-4 text-gray-600 dark:text-gray-400">
			<div class="grid gap-6 md:grid-cols-3">
				<p>© {{ new Date().getFullYear() }} {{ appName }}. All rights reserved.</p>
				<nav class="flex gap-4">
					<RouterLink to="/about" class="hover:underline">Giới thiệu</RouterLink>
					<RouterLink to="/contact" class="hover:underline">Liên hệ</RouterLink>
					<RouterLink to="/policy" class="hover:underline">Chính sách</RouterLink>
				</nav>
				<p class="text-right md:text-left">Theo dõi: <a href="#" class="hover:underline">Facebook</a> · <a href="#" class="hover:underline">Instagram</a></p>
			</div>
		</div>
	</footer>
</template>

<script setup>
import { APP_NAME } from '../../utils/constants';
const appName = APP_NAME;
</script>


