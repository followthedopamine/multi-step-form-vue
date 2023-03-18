<script lang="ts" setup>
import TextInput from './TextInput.vue'
import LargeRadioButton from './LargeRadioButton.vue'
import RoundedCheckboxToggle from './RoundedCheckboxToggle.vue'
import LargeRoundedCheckbox from './LargeRoundedCheckbox.vue'
const props = defineProps({
  currentStep: Number
})

let yearly = false

const monthlyYearlyToggle = () => {
  yearly = !yearly
  console.log(yearly)
}
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

        <TextInput input-id="name" label-text="Name" placeholder="e.g. Stephen King" />
        <TextInput
          input-id="email"
          label-text="Email Address"
          placeholder="e.g. stephenking@lorem.com"
        />
        <TextInput input-id="phone" label-text="Phone Number" placeholder="e.g. +1 234 567 890" />
      </div>

      <div v-show="currentStep === 2" id="step-2">
        <h1 class="text-marine-blue font-bold text-2xl mb-4">Select your plan</h1>
        <h2 class="h1 text-cool-gray mb-4">You have the option of monthly or yearly billing.</h2>
        <div class="radios">
          <LargeRadioButton value="arcade" label="Arcade" text="$9/mo" name="plan" />
          <LargeRadioButton value="advanced" label="Advanced" text="$12/mo" name="plan" />
          <LargeRadioButton value="pro" label="Pro" text="$15/mo" name="plan" />
        </div>
        <RoundedCheckboxToggle @toggle-changed="monthlyYearlyToggle" />
      </div>

      <div v-show="currentStep === 3" id="step-3">
        <h1 class="text-marine-blue font-bold text-2xl mb-4">Pick add-ons</h1>
        <h2 class="h1 text-cool-gray mb-4">Add-ons help enhance your gaming experience.</h2>
        <div class="checkboxes">
          <LargeRoundedCheckbox />
          <!-- <div>
            <input
              id="online-service"
              type="checkbox"
              class="accent-purplish-blue w-5 h-5 m-4 cursor-pointer absolute mt-7"
            />
            <label
              for="online-service"
              class="cursor-pointer flex items-center w-full border border-light-gray rounded-lg h-20 mb-4"
            >
              <label for="online-service" class="cursor-pointer ml-14 h-full">
                <div class="h-full flex items-center">
                  <div class="w-11/12 float-left -mt-2">
                    <div class="text-marine-blue font-medium text-lg text-[1.05rem] tracking-tight">
                      Online service
                    </div>
                    <div class="text-cool-gray text-xs tracking-tight w-11/12">
                      Access to multiplayer games
                    </div>
                  </div>
                  <div class="w-1/12 float-right text-purplish-blue text-sm h-full">
                    <div class="flex items-center h-full -ml-3 font-medium"><div>+$1/mo</div></div>
                  </div>
                </div>
              </label>
            </label>
          </div> -->
        </div>
      </div>
    </form>
  </div>
</template>

<style scoped>
.chk:checked + .chk-label {
  background-color: violet;
}

.chk:unchecked + .unchk-label {
  background-color: violet;
}

.chk-label {
  background-color: blue;
}

.checkboxes input[type='checkbox']:checked + label {
  border-color: #544c97;
  background-color: #f8f9fe;
}
</style>
