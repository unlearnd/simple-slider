<script setup lang="ts">
import { ref } from 'vue';

const stepValue = ref(0);
const currentValue = ref(0);
const minValue = ref(0);
const maxValue = ref(100);
</script>

<template>
	<div class="slider-container">
		<div class="container">
			<v-slider
				class="main-item"
				v-model="currentValue"
				label="Test Control"
				:max="maxValue"
				:min="minValue"
				:step="stepValue">
			</v-slider>
			<v-text-field
				class="peripheral-item"
				label="Current Value"
				readonly
				v-model="currentValue"></v-text-field>
		</div>

		<div class="container">
			<v-text-field
				class="item"
				label="Step Value"
				v-model="stepValue"></v-text-field>
			<v-text-field
				class="item"
				label="Minimum Value"
				v-model="minValue"></v-text-field>
			<v-text-field
				class="item"
				label="Maximum Value"
				v-model="maxValue"></v-text-field>
		</div>
	</div>
</template>

<style scoped>
.slider-container {
	justify-content: center;
	width: 90vw;
}

.main-item {
	width: 70%;
}

.peripheral-item {
	width: 30%;
}
.container {
	display: flex;
}
.item {
	margin-top: 1rem;
	flex: 3 1 auto;
	width: max-content;
	margin: 1rem;
	justify-items: space-between;
}
</style>
