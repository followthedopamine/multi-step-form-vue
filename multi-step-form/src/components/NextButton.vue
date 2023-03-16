<script lang="ts" setup>
import { ref } from 'vue'

const props = defineProps({
  currentStep: Number
})

const emit = defineEmits(['nextStep'])

const lastStep = 4

const handleNextStep = () => {
  if (props.currentStep !== lastStep) emit('nextStep')
}
</script>

<template>
  <button @click="handleNextStep" class="p-2 px-4 bg-marine-blue text-white rounded self-end mr-4">
    {{ props.currentStep !== lastStep ? 'Next Step' : 'Confirm' }}
  </button>
</template>
