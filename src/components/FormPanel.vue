<script lang="ts" setup>
import FormStep1 from './FormStep1.vue'
import FormStep2 from './FormStep2.vue'
import FormStep3 from './FormStep3.vue'
import FormStep4 from './FormStep4.vue'
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
      <FormStep1 v-show="props.currentStep === 1" />
      <FormStep2
        v-show="props.currentStep === 2"
        :data="data"
        @change-plan="changePlan"
        @monthly-yearly-toggle="monthlyYearlyToggle"
      />
      <FormStep3
        v-show="props.currentStep === 3"
        :data="data"
        @toggle-checked-checkbox="toggleCheckedCheckbox"
      />
      <FormStep4 v-show="props.currentStep === 4" :data="data" :options="options" @step2="step2" />
    </form>
  </div>
</template>

<style scoped></style>
