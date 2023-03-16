<script lang="ts" setup>
import { defineEmits } from 'vue'

const props = defineProps({
  step: Number,
  currentStep: Number
})

const emit = defineEmits(['changeStep'])

const handleChangeStep = () => {
  emit('changeStep', props.step)
}
</script>

<template>
  <button
    @click="handleChangeStep"
    class="text-marine-blue bg-light-blue rounded-full w-8 h-8 font-medium"
    v-if="step === currentStep"
  >
    {{ props.step }}
  </button>
  <button
    @click="handleChangeStep"
    class="text-white border rounded-full w-8 h-8 font-medium"
    v-if="step !== currentStep"
  >
    {{ props.step }}
  </button>
</template>
