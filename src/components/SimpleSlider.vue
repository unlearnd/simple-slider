<template>
	<div class="slider-container">
		<input
			type="range"
			:min="minValue"
			:max="maxValue"
			:value="currentValue"
			:step="stepValue"
			@input="
				$emit(
					'update:modelValue',
					(currentValue = parseInt(
						($event.target as HTMLInputElement)?.value ?? 0,
						10
					))
				)
			" />
		<div class="slider-steps">
			<span :class="showStepLabels ? 'slider-step' : ''" v-for="step in steps">
				<span v-if="showStepLabels" class="slider-step-label"> {{ step }}</span>
			</span>
		</div>
	</div>
</template>

<script setup lang="ts">
import { ref, computed, type PropType } from 'vue';

const props = defineProps({
	stepValue: { type: Number as PropType<number>, default: 1, required: true },
	modelValue: { type: Number as PropType<number>, default: 0, required: true },
	minValue: { type: Number as PropType<number>, default: 0, required: true },
	maxValue: { type: Number as PropType<number>, default: 100, required: true },
	showStepLabels: {
		type: Boolean as PropType<boolean>,
		default: false,
		required: true,
	},
});

const currentValue = ref(props.modelValue);

const emit = defineEmits<{
	(e: 'update:modelValue', value: number): void;
}>();

const steps = computed(() => {
	// Do some very basic checks around min/max/step values before computing the step list.
	const firstStep =
		props.minValue > props.maxValue ? props.maxValue : props.minValue;
	const lastStep = props.maxValue < firstStep ? firstStep : props.maxValue;
	const useStepSize = props.stepValue > 0 ? props.stepValue : 1;
	const computedSteps = [];

	let currentStep = firstStep;

	while (currentStep <= lastStep) {
		computedSteps.push(currentStep);
		currentStep += useStepSize;
	}

	return computedSteps;
});
</script>
<style scoped>
input[type='range'] {
	/* Ensure the control uses the available width */
	width: 100%;
}

.slider-container {
	justify-content: center;
	width: 90vw;
}

.slider-steps {
	display: flex;
	justify-content: space-between;
	padding: 0 10px;
	min-height: 2rem;
}

.slider-steps span.slider-step {
	display: flex;
	justify-content: center;
	width: 1px;
	height: 10px;
	background: #d3d3d3;
	line-height: 40px;
}
</style>
