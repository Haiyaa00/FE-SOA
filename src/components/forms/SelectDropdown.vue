<template>
	<label class="block text-sm">
		<span v-if="label" class="mb-1 block font-medium">{{ label }}</span>
		<select
			class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-gray-900 focus:ring-gray-900 dark:border-gray-700 dark:bg-gray-900 dark:text-gray-100"
			:value="modelValue"
			@change="$emit('update:modelValue', $event.target.value)"
		>
			<option v-for="o in options" :key="o.value" :value="o.value">{{ o.label }}</option>
		</select>
	</label>
</template>

<script setup>
defineProps({
	modelValue: [String, Number],
	label: String,
	options: {
		type: Array,
		default: () => []
	}
});
defineEmits(['update:modelValue']);
</script>


