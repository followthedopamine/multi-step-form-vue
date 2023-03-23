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
  <button
    @click="handleNextStep"
    class="p-2 px-4 text-white rounded mr-4 ml-auto"
    :class="{
      'bg-marine-blue': props.currentStep !== lastStep,
      'bg-purplish-blue': props.currentStep === lastStep
    }"
  >
    {{ props.currentStep !== lastStep ? 'Next Step' : 'Confirm' }}
  </button>
</template>
