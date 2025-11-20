<template>
	<section class="mx-auto max-w-2xl">
		<button @click="goBack" class="mb-2 text-sm text-gray-500 hover:underline">← Quay lại</button>
		<h1 class="mb-4 text-xl font-semibold">Hồ sơ cá nhân</h1>
		<div class="space-y-4 rounded-lg border p-4 dark:border-gray-800">
			<div>
				<p class="text-sm text-gray-500">Tên</p>
				<p class="font-medium">{{ user.profile?.name }}</p>
			</div>
			<div>
				<p class="text-sm text-gray-500">Email</p>
				<p class="font-medium">{{ user.profile?.email }}</p>
			</div>
		</div>
		<form class="mt-6 space-y-3 rounded-lg border p-4 dark:border-gray-800" @submit.prevent="save">
			<h2 class="font-semibold">Chỉnh sửa</h2>
			<InputField v-model="form.name" label="Tên" />
			<InputField v-model="form.email" label="Email" type="email" />
			<button class="rounded bg-gray-900 px-3 py-2 text-white dark:bg-gray-100 dark:text-black">Lưu</button>
		</form>
	</section>
</template>

<script setup>
import { reactive } from 'vue';
import { useUserStore } from '../stores/user';
import { useUIStore } from '../stores/ui';
import { useRouter } from 'vue-router';
import InputField from '../components/forms/InputField.vue';

const user = useUserStore();
const ui = useUIStore();
const router = useRouter();
const form = reactive({ name: user.profile?.name ?? '', email: user.profile?.email ?? '' });

function save() {
	user.updateProfile(form);
	ui.pushToast({ type: 'success', message: 'Cập nhật thành công' });
}
function goBack() {
	router.back();
}
</script>


