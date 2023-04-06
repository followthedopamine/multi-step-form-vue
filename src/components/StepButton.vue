<script lang="ts" setup>
import { defineEmits } from 'vue'

const props = defineProps({
  step: Number,
  currentStep: Number,
  text: String
})

const emit = defineEmits(['changeStep'])

const handleChangeStep = () => {
  emit('changeStep', props.step)
}
</script>

<template>
  <span>
    <div class="flex flex-row md:px-10 md:py-4">
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
      <span class="hidden md:flex flex-col pl-4" @click="handleChangeStep">
        <span class="text-cool-gray text-xs">STEP {{ props.step }}</span>
        <span class="text-white text-sm font-bold">{{ props.text }}</span>
      </span>
    </div>
  </span>
</template>
