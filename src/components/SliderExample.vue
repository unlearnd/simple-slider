<template>
	<div class="main-container">
		<div class="item-container">
			<label class="label" for="slider"> Test Control </label>
			<SimpleSlider
				id="slider"
				class="main-item"
				v-model="currentValue"
				:max-value="maxValue"
				:min-value="minValue"
				:show-step-labels="showStepLabels"
				:step-value="stepValue">
			</SimpleSlider>
		</div>
		<div class="item-container">
			<label class="label" for="current-value">Current Value</label>
			<input
				id="current-value"
				readonly
				class="peripheral-item"
				:value="currentValue" />
		</div>
	</div>
	<div class="settings-container">
		<div class="item-container-fit">
			<label class="label" for="show-step-labels">Show Step Labels</label>
			<input type="checkbox" id="step-step-labels" v-model="showStepLabels" />
		</div>
		<div class="item-container-fit">
			<label class="label" for="min-value">Min Value</label>
			<input id="min-value" type="number" :max="maxValue" v-model="minValue" />
		</div>
		<div class="item-container-fit">
			<label class="label" for="max-value">Max Value</label>
			<input id="max-value" type="number" v-model="maxValue" />
		</div>
		<div class="item-container-fit">
			<label class="label" for="step-value">Step Value</label>
			<input id="step-value" type="number" v-model="stepValue" />
		</div>
	</div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import SimpleSlider from './SimpleSlider.vue';

const currentValue = ref(0);
const minValue = ref(0);
const maxValue = ref(100);
const showStepLabels = ref(false);
const stepValue = ref(5);
</script>
<style scoped>
.main-container {
	width: 90vw;
	display: flex;
}

.item-container {
	width: 100%;
	display: flex;
	flex-direction: column;
}

.settings-container {
	display: flex;
	justify-content: start;
}

.item-container-fit {
	display: flex;
	padding-left: 2rem;
	flex-direction: column;
}

label {
	margin-bottom: 0.15rem;
}

.main-item {
	width: 80%;
}

.peripheral-item {
	width: 20%;
}

.item {
	margin-top: 1rem;
	flex: 3 1 auto;
	width: max-content;
	margin: 1rem;
	justify-items: space-between;
}
</style>
