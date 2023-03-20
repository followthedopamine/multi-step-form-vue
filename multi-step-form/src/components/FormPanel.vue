<script lang="ts" setup>
import TextInput from './TextInput.vue'
import LargeRadioButton from './LargeRadioButton.vue'
import RoundedCheckboxToggle from './RoundedCheckboxToggle.vue'
import LargeRoundedCheckbox from './LargeRoundedCheckbox.vue'
import { ref } from 'vue'
const props = defineProps({
  currentStep: Number
})

const monthlyYearlyToggle = () => {
  data.value.yearly = !data.value.yearly
}

enum plans {
  arcade,
  advanced,
  pro
}

const options: Object = {
  onlineService: {
    name: 'Online service',
    price: 1
  },
  largerStorage: {
    name: 'Larger storage',
    price: 2
  },
  customizableProfile: {
    name: 'Customizable profile',
    price: 2
  }
}

const data = ref({
  plan: plans.arcade,
  yearly: false,
  options: [0]
})
</script>

<template>
  <div class="bg-white p-7 w-11/12 absolute -mt-16 rounded-lg drop-shadow">
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
          <LargeRadioButton
            value="arcade"
            label="Arcade"
            :text="data.yearly ? '$90/yr' : '$9/mo'"
            :sub-text="data.yearly ? '2 months free' : ''"
            name="plan"
            checked
          />
          <LargeRadioButton
            value="advanced"
            label="Advanced"
            :text="data.yearly ? '$120/yr' : '$12/mo'"
            :sub-text="data.yearly ? '2 months free' : ''"
            name="plan"
          />
          <LargeRadioButton
            value="pro"
            label="Pro"
            :text="data.yearly ? '$150/yr' : '$15/mo'"
            :sub-text="data.yearly ? '2 months free' : ''"
            name="plan"
          />
        </div>
        <RoundedCheckboxToggle @toggle-changed="monthlyYearlyToggle" />
      </div>

      <div v-show="currentStep === 3" id="step-3">
        <h1 class="text-marine-blue font-bold text-2xl mb-4">Pick add-ons</h1>
        <h2 class="h1 text-cool-gray mb-4">Add-ons help enhance your gaming experience.</h2>
        <div class="checkboxes">
          <LargeRoundedCheckbox
            name="online-service"
            value="online"
            label="Online service"
            text="Access to multiplayer games"
            :price="data.yearly ? '+$10/yr' : '+$1/mo'"
          />
          <LargeRoundedCheckbox
            name="larger-storage"
            value="larger"
            label="Larger storage"
            text="Extra 1TB of cloud save"
            :price="data.yearly ? '+$20/yr' : '+$2/mo'"
          />
          <LargeRoundedCheckbox
            name="customizable-profile"
            value="profile"
            label="Customizable profile"
            text="Custom theme on your profile"
            :price="data.yearly ? '+$20/yr' : '+$2/mo'"
          />
        </div>
      </div>
      <div v-show="currentStep === 4" id="step-4">
        <h1 class="text-marine-blue font-bold text-2xl mb-4">Finishing up</h1>
        <h2 class="h1 text-cool-gray mb-4">Double-check everything looks OK before confirming.</h2>
        <div class="bg-magnolia rounded p-4">
          <div class="flex text-marine-blue pb-3">
            <div>
              <div class="font-medium">Arcade (Monthly)</div>
              <div class="text-cool-gray underline">Change</div>
            </div>
            <div class="ml-auto font-bold flex items-end mb-2"><div>$9/mo</div></div>
          </div>
          <hr class="border-light-gray mb-2" />
          <ul>
            <li class="flex py-1 text-cool-gray text-base">
              <div>
                <div>Online service</div>
              </div>
              <div class="ml-auto text-marine-blue">+$1/mo</div>
            </li>
            <li class="flex py-1 text-cool-gray text-base">
              <div>
                <div>Larger storage</div>
              </div>
              <div class="ml-auto text-marine-blue">+$2/mo</div>
            </li>
          </ul>
        </div>

        <div class="p-4 flex">
          <div class="mt-0.5 text-cool-gray">Total (per month)</div>
          <div class="ml-auto text-purplish-blue font-bold text-lg">+$12/mo</div>
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
</style>
