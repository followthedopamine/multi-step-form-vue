<script lang="ts" setup>
import TextInput from './TextInput.vue'
const props = defineProps({
  currentStep: Number
})
</script>

<template>
  <div class="bg-white p-8 w-11/12 absolute -mt-16 rounded-lg drop-shadow">
    <form action="">
      <!-- Hide this for step 2 - 5 -->
      <div v-show="currentStep === 1" id="step-1">
        <h1 class="text-marine-blue font-bold text-2xl mb-4">Personal info</h1>
        <h2 class="h1 text-cool-gray mb-4">
          Please provide your name, email address, and phone number.
        </h2>

        <TextInput input-id="name" label-text="Name" placeholder="e.g. Stephen King"></TextInput>
        <TextInput
          input-id="email"
          label-text="Email Address"
          placeholder="e.g. stephenking@lorem.com"
        ></TextInput>
        <TextInput
          input-id="phone"
          label-text="Phone Number"
          placeholder="e.g. +1 234 567 890"
        ></TextInput>
      </div>

      <div v-show="currentStep === 2" id="step-2">
        <h1 class="text-marine-blue font-bold text-2xl mb-4">Select your plan</h1>
        <h2 class="h1 text-cool-gray mb-4">You have the option of monthly or yearly billing.</h2>

        <TextInput input-id="name" label-text="Name" placeholder="e.g. Stephen King"></TextInput>
        <TextInput
          input-id="email"
          label-text="Email Address"
          placeholder="e.g. stephenking@lorem.com"
        ></TextInput>
        <TextInput
          input-id="phone"
          label-text="Phone Number"
          placeholder="e.g. +1 234 567 890"
        ></TextInput>
      </div>
    </form>
  </div>
</template>
