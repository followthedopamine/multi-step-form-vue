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
  <div class="flex flex-col md:items-center h-full w-[375px] max-h-[700px] md:w-full md:mt-40">
    <div class="md:z-20 md:max-w-[878px] md:w-11/12 md:pl-5 md:pointer-events-none">
      <header class="h-40 flex justify-center md:w-[274px] md:h-[568px] md:pointer-events-auto">
        <div class="mt-8 w-5/12 flex justify-between md:w-full md:justify-start md:flex-col">
          <StepButton
            @changeStep="changeStep"
            :step="1"
            :current-step="currentStep"
            text="YOUR INFO"
          />
          <StepButton
            @changeStep="changeStep"
            :step="2"
            :current-step="currentStep"
            text="SELECT PLAN"
          />

          <StepButton
            @changeStep="changeStep"
            :step="3"
            :current-step="currentStep"
            text="ADD-ONS"
          />
          <StepButton
            @changeStep="changeStep"
            :step="4"
            :current-step="currentStep"
            text="SUMMARY"
          />
        </div>
      </header>
    </div>
    <main class="flex-col flex-grow flex items-center bg-light-gray md:bg-opacity-0">
      <FormPanel :current-step="currentStep" @step2="changeStep(2)" />
    </main>
    <div class="md:w-11/12 md:z-10 md:absolute md:flex md:justify-center md:max-w-[878px]">
      <footer
        class="h-16 py-10 flex items-center bg-white md:top-[500px] md:relative md:left-36 md:w-[48%]"
      >
        <BackButton @prev-step="prevStep" :current-step="currentStep" />
        <NextButton class="" @next-step="nextStep" :current-step="currentStep" />
      </footer>
    </div>
  </div>
</template>

<style scoped>
header {
  background-image: url('assets/images/bg-sidebar-mobile.svg');
}

@media screen and (min-width: 768px) {
  header {
    background-image: url('assets/images/bg-sidebar-desktop.svg');
  }
}
</style>
