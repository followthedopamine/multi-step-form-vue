<script setup lang="ts">
import NextButton from './components/NextButton.vue'
import FormPanel from './components/FormPanel.vue'
import StepButton from './components/StepButton.vue'
import BackButton from './components/BackButton.vue'
import { ref } from 'vue'

const currentStep = ref(1)
const name = ref('')
const email = ref('')
const phone = ref('')
const errors = ref({ name: '', email: '', phone: '' })

const changeStep = (newStep: number) => {
  if (!validateForm()) return
  currentStep.value = newStep
}

const nextStep = () => {
  if (!validateForm()) return
  currentStep.value++
}

const prevStep = () => {
  currentStep.value--
}

const updateName = (newName: string) => {
  name.value = newName
  validateName()
}

const updateEmail = (newEmail: string) => {
  email.value = newEmail
  validateEmail()
}

const updatePhone = (newPhone: string) => {
  phone.value = newPhone
  validatePhone()
}

const validateName = (): boolean => {
  if (name.value.length > 0) {
    errors.value.name = ''
    return true
  } else {
    errors.value.name = 'Name is invalid'
    return false
  }
}

const validateEmail = (): boolean => {
  if (email.value.length > 0) {
    errors.value.email = ''
    return true
  } else {
    errors.value.email = 'Email is invalid'
    return false
  }
}

const validatePhone = (): boolean => {
  if (phone.value.length > 6) {
    errors.value.phone = ''
    return true
  } else {
    errors.value.phone = 'Phone is invalid'
    return false
  }
}

const validateForm = (): boolean => {
  let isValid: boolean = true
  if (currentStep.value == 1) {
    if (!validateName()) isValid = false
    if (!validateEmail()) isValid = false
    if (!validatePhone()) isValid = false
  }
  return isValid
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
      <FormPanel
        :current-step="currentStep"
        @step2="changeStep(2)"
        @update-name="updateName"
        @update-email="updateEmail"
        @update-phone="updatePhone"
        :errors="errors"
      />
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
