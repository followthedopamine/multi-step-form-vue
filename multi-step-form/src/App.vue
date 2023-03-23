<script setup lang="ts">
import NextButton from './components/NextButton.vue'
import FormPanel from './components/FormPanel.vue'
import StepButton from './components/StepButton.vue'
import BackButton from './components/BackButton.vue'
import { ref } from 'vue'

const currentStep = ref(1)

const changeStep = (newStep: number) => {
  currentStep.value = newStep
}

const nextStep = () => {
  currentStep.value++
}

const prevStep = () => {
  currentStep.value--
}
</script>

<template>
  <div class="flex flex-col h-full">
    <header class="h-40 flex justify-center">
      <div class="mt-8 w-5/12 flex justify-between">
        <StepButton
          @changeStep="(newStep) => changeStep(newStep)"
          :step="1"
          :current-step="currentStep"
        ></StepButton>
        <StepButton
          @changeStep="(newStep) => changeStep(newStep)"
          :step="2"
          :current-step="currentStep"
        ></StepButton>
        <StepButton
          @changeStep="(newStep) => changeStep(newStep)"
          :step="3"
          :current-step="currentStep"
        ></StepButton>
        <StepButton
          @changeStep="(newStep) => changeStep(newStep)"
          :step="4"
          :current-step="currentStep"
        ></StepButton>
      </div>
    </header>
    <main class="flex-col flex-grow flex items-center bg-light-gray">
      <FormPanel :current-step="currentStep" @step2="changeStep(2)"></FormPanel>
    </main>
    <footer class="h-16 py-10 flex items-center">
      <BackButton @prev-step="prevStep" :current-step="currentStep" />
      <NextButton @next-step="nextStep" :current-step="currentStep" />
    </footer>
  </div>
</template>

<style scoped>
header {
  background-image: url('assets/images/bg-sidebar-mobile.svg');
}
</style>
