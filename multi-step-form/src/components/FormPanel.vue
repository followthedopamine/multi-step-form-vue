<script lang="ts" setup>
import TextInput from './TextInput.vue'
import LargeRadioButton from './LargeRadioButton.vue'
import RoundedCheckboxToggle from './RoundedCheckboxToggle.vue'
import LargeRoundedCheckbox from './LargeRoundedCheckbox.vue'
import { ref } from 'vue'
const props = defineProps({
  currentStep: Number
})

const emit = defineEmits(['step2'])

const monthlyYearlyToggle = () => {
  data.value.yearly = !data.value.yearly
  updateTotal()
}

interface Plan {
  name: string
  price: number
  display: string
}

const plans: Plan[] = [
  {
    name: 'arcade',
    display: 'Arcade',
    price: 9
  },
  {
    name: 'advanced',
    display: 'Advanced',
    price: 12
  },
  {
    name: 'pro',
    display: 'Pro',
    price: 15
  }
]

interface Option {
  name: string
  price: number
}

const options: Option[] = [
  {
    name: 'Online service',
    price: 1
  },
  {
    name: 'Larger storage',
    price: 2
  },
  {
    name: 'Customizable profile',
    price: 2
  }
]

const updateTotal = () => {
  let res = 0
  res += data.value.plan.price
  data.value.options.forEach((index: number) => {
    res += options[index].price
  })
  if (data.value.yearly) {
    res *= 10
  }
  data.value.total = res
}

const data = ref({
  plan: plans[0],
  yearly: false,
  options: new Set<number>(),
  total: plans[0].price
})

const toggleCheckedCheckbox = (checked: Boolean, index: number) => {
  if (checked) {
    data.value.options.add(index)
  } else {
    if (data.value.options.has(index)) data.value.options.delete(index)
  }
  updateTotal()
}

const changePlan = (checked: Boolean, index: number) => {
  data.value.plan = plans[index]
  updateTotal()
}

const step2 = () => {
  emit('step2')
}
</script>

<template>
  <div class="bg-white p-7 w-11/12 absolute -mt-16 rounded-lg drop-shadow">
    <form action="">
      <!-- Hide this for step 2 - 5 -->
      <div v-show="props.currentStep === 1" id="step-1">
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

      <div v-show="props.currentStep === 2" id="step-2">
        <h1 class="text-marine-blue font-bold text-2xl mb-4">Select your plan</h1>
        <h2 class="h1 text-cool-gray mb-4">You have the option of monthly or yearly billing.</h2>
        <div class="radios">
          <LargeRadioButton
            value="arcade"
            label="Arcade"
            :text="data.yearly ? '$90/yr' : '$9/mo'"
            :sub-text="data.yearly ? '2 months free' : ''"
            :index="0"
            name="plan"
            @checked-changed="changePlan"
            checked
          />
          <LargeRadioButton
            value="advanced"
            label="Advanced"
            :text="data.yearly ? '$120/yr' : '$12/mo'"
            :sub-text="data.yearly ? '2 months free' : ''"
            :index="1"
            name="plan"
            @checked-changed="changePlan"
          />
          <LargeRadioButton
            value="pro"
            label="Pro"
            :text="data.yearly ? '$150/yr' : '$15/mo'"
            :sub-text="data.yearly ? '2 months free' : ''"
            :index="2"
            name="plan"
            @checked-changed="changePlan"
          />
        </div>
        <RoundedCheckboxToggle @toggle-changed="monthlyYearlyToggle" />
      </div>

      <div v-show="props.currentStep === 3" id="step-3">
        <h1 class="text-marine-blue font-bold text-2xl mb-4">Pick add-ons</h1>
        <h2 class="h1 text-cool-gray mb-4">Add-ons help enhance your gaming experience.</h2>
        <div class="checkboxes">
          <LargeRoundedCheckbox
            name="online-service"
            value="online"
            label="Online service"
            text="Access to multiplayer games"
            :price="data.yearly ? '+$10/yr' : '+$1/mo'"
            :index="0"
            @toggle-checked="toggleCheckedCheckbox"
          />
          <LargeRoundedCheckbox
            name="larger-storage"
            value="larger"
            label="Larger storage"
            text="Extra 1TB of cloud save"
            :price="data.yearly ? '+$20/yr' : '+$2/mo'"
            :index="1"
            @toggle-checked="toggleCheckedCheckbox"
          />
          <LargeRoundedCheckbox
            name="customizable-profile"
            value="profile"
            label="Customizable profile"
            text="Custom theme on your profile"
            :price="data.yearly ? '+$20/yr' : '+$2/mo'"
            :index="2"
            @toggle-checked="toggleCheckedCheckbox"
          />
        </div>
      </div>
      <div v-show="props.currentStep === 4" id="step-4">
        <h1 class="text-marine-blue font-bold text-2xl mb-4">Finishing up</h1>
        <h2 class="h1 text-cool-gray mb-4">Double-check everything looks OK before confirming.</h2>
        <div class="bg-magnolia rounded p-4">
          <div class="flex text-marine-blue pb-3">
            <div>
              <div class="font-medium">
                {{ data.plan.display }} {{ !data.yearly ? '(Monthly)' : '(Yearly)' }}
              </div>
              <a
                class="text-cool-gray underline cursor-pointer hover:text-purplish-blue hover:decoration-2"
                @click="step2"
                >Change</a
              >
            </div>
            <div class="ml-auto font-bold flex items-end mb-2">
              <div>
                ${{ !data.yearly ? data.plan.price + '/mo' : data.plan.price * 10 + '/ye' }}
              </div>
            </div>
          </div>
          <hr v-show="data.options.size" class="border-light-gray mb-2" />
          <ul>
            <li
              v-for="index in data.options"
              :key="'index' + index"
              class="flex py-1 text-cool-gray text-base"
            >
              <div>
                <div>{{ options[index].name }}</div>
              </div>
              <div class="ml-auto text-marine-blue">
                ${{
                  !data.yearly ? options[index].price + '/mo' : options[index].price * 10 + '/ye'
                }}
              </div>
            </li>
          </ul>
        </div>

        <div class="p-4 flex">
          <div class="mt-0.5 text-cool-gray">
            Total {{ !data.yearly ? '(per month)' : '(per year)' }}
          </div>
          <div class="ml-auto text-purplish-blue font-bold text-lg">
            +${{ data.total }}/{{ !data.yearly ? 'mo' : 'yr' }}
          </div>
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
