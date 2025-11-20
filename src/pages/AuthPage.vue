<template>
	<section class="mx-auto max-w-md">
		<h1 class="mb-4 text-center text-xl font-semibold">Đăng nhập / Đăng ký</h1>
		<div class="grid gap-6 md:grid-cols-2">
			<form class="space-y-3 rounded-lg border p-4 dark:border-gray-800" @submit.prevent="login">
				<h2 class="font-semibold">Đăng nhập</h2>
				<InputField v-model="loginForm.email" label="Email" type="email" />
				<InputField v-model="loginForm.password" label="Mật khẩu" type="password" />
				<button type="submit" class="w-full rounded bg-gray-900 px-3 py-2 text-white dark:bg-gray-100 dark:text-black">Đăng nhập</button>
			</form>
			<form class="space-y-3 rounded-lg border p-4 dark:border-gray-800" @submit.prevent="register">
				<h2 class="font-semibold">Đăng ký</h2>
				<InputField v-model="registerForm.name" label="Họ tên" />
				<InputField v-model="registerForm.email" label="Email" type="email" />
				<InputField v-model="registerForm.password" label="Mật khẩu" type="password" />
				<InputField v-model="registerForm.confirm" label="Xác nhận mật khẩu" type="password" />
				<button type="submit" class="w-full rounded bg-gray-900 px-3 py-2 text-white dark:bg-gray-100 dark:text-black">Tạo tài khoản</button>
			</form>
		</div>
	</section>
</template>

<script setup>
import { reactive } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import { useUserStore } from '../stores/user';
import { useUIStore } from '../stores/ui';
import InputField from '../components/forms/InputField.vue';

const route = useRoute();
const router = useRouter();
const user = useUserStore();
const ui = useUIStore();

const loginForm = reactive({ email: '', password: '' });
const registerForm = reactive({ name: '', email: '', password: '', confirm: '' });

async function login() {
	// Demo login
	// Check if email is admin email
	const isAdmin = loginForm.email === 'admin@example.com';
	user.login({
		token: 'demo-token',
		profile: { id: 1, name: isAdmin ? 'Admin' : 'Demo User', email: loginForm.email },
		role: isAdmin ? 'admin' : 'user'
	});
	ui.pushToast({ type: 'success', message: 'Đăng nhập thành công' });
	const redirect = route.query.redirect || '/';
	router.replace(String(redirect));
}

async function register() {
	if (registerForm.password !== registerForm.confirm) {
		ui.pushToast({ type: 'error', message: 'Mật khẩu không khớp' });
		return;
	}
	// Check if email is admin email
	const isAdmin = registerForm.email === 'admin@example.com';
	user.login({
		token: 'demo-token',
		profile: { id: 2, name: registerForm.name, email: registerForm.email },
		role: isAdmin ? 'admin' : 'user'
	});
	ui.pushToast({ type: 'success', message: 'Tạo tài khoản thành công' });
	router.replace('/');
}
</script>


