<template>
	<section>
		<button @click="goBack" class="mb-2 text-sm text-gray-500 hover:underline">← Quay lại</button>
		<h1 class="mb-4 text-xl font-semibold">Thanh toán</h1>
		<div class="mb-4 flex items-center gap-2 text-sm text-gray-500">
			<span class="rounded bg-gray-200 px-2 py-0.5 dark:bg-gray-800">Giỏ hàng</span> →
			<span class="rounded bg-gray-900 px-2 py-0.5 text-white dark:bg-gray-100 dark:text-black">Địa chỉ</span> →
			<span class="rounded bg-gray-200 px-2 py-0.5 dark:bg-gray-800">Thanh toán</span> →
			<span class="rounded bg-gray-200 px-2 py-0.5 dark:bg-gray-800">Hoàn tất</span>
		</div>
		<div class="grid gap-6 md:grid-cols-[1fr_360px]">
			<form class="space-y-3">
				<InputField v-model="form.name" label="Họ và tên" />
				<InputField v-model="form.phone" label="Số điện thoại" />
				<InputField v-model="form.address" label="Địa chỉ" />
				<SelectDropdown v-model="form.payment" label="Phương thức thanh toán" :options="payments" />
				<InputField v-model="form.voucher" label="Voucher" placeholder="Nhập mã giảm giá (tùy chọn)" />
				<button type="button" class="rounded bg-gray-900 px-4 py-2 text-white dark:bg-gray-100 dark:text-black" @click="placeOrder">
					Đặt hàng
				</button>
			</form>
			<aside class="rounded-lg border p-4 dark:border-gray-800">
				<h2 class="mb-3 font-semibold">Tóm tắt đơn hàng</h2>
				<p class="text-sm text-gray-500">Số lượng: {{ count }} sản phẩm</p>
				<p class="mt-2 text-xl font-bold">{{ formatCurrency(subtotal) }}</p>
			</aside>
		</div>
	</section>
</template>

<script setup>
import { reactive, computed } from 'vue';
import { useRouter } from 'vue-router';
import { useCartStore } from '../stores/cart';
import { useUIStore } from '../stores/ui';
import { formatCurrency } from '../utils/helpers';
import InputField from '../components/forms/InputField.vue';
import SelectDropdown from '../components/forms/SelectDropdown.vue';

const cart = useCartStore();
const ui = useUIStore();
const router = useRouter();

const form = reactive({ name: '', phone: '', address: '', payment: 'cod', voucher: '' });
const payments = [
	{ value: 'cod', label: 'Thanh toán khi nhận hàng (COD)' },
	{ value: 'momo', label: 'Momo (demo)' }
];

const count = computed(() => cart.itemCount);
const subtotal = computed(() => cart.subtotal);

function placeOrder() {
	if (!count.value) {
		ui.pushToast({ type: 'error', message: 'Giỏ hàng trống' });
		return;
	}
	ui.pushToast({ type: 'success', message: 'Đặt hàng thành công (demo)' });
	cart.clear();
	router.push('/orders');
}
function goBack() {
	router.back();
}
</script>


