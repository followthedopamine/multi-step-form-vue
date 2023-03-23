<script lang="ts" setup>
import LargeRadioButton from './LargeRadioButton.vue'
import RoundedCheckboxToggle from './RoundedCheckboxToggle.vue'

const props = defineProps({
  data: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['changePlan', 'monthlyYearlyToggle'])

const changePlan = (checked: Boolean, index: number) => {
  emit('changePlan', checked, index)
}

const monthlyYearlyToggle = () => {
  emit('monthlyYearlyToggle')
}
</script>

<template>
  <div id="step-2">
    <h1 class="text-marine-blue font-bold text-2xl mb-4">Select your plan</h1>
    <h2 class="h1 text-cool-gray mb-4">You have the option of monthly or yearly billing.</h2>
    <div class="radios">
      <LargeRadioButton
        value="arcade"
        label="Arcade"
        :text="props.data.yearly ? '$90/yr' : '$9/mo'"
        :sub-text="props.data.yearly ? '2 months free' : ''"
        :index="0"
        name="plan"
        @checked-changed="changePlan"
        checked
      />
      <LargeRadioButton
        value="advanced"
        label="Advanced"
        :text="props.data.yearly ? '$120/yr' : '$12/mo'"
        :sub-text="props.data.yearly ? '2 months free' : ''"
        :index="1"
        name="plan"
        @checked-changed="changePlan"
      />
      <LargeRadioButton
        value="pro"
        label="Pro"
        :text="props.data.yearly ? '$150/yr' : '$15/mo'"
        :sub-text="props.data.yearly ? '2 months free' : ''"
        :index="2"
        name="plan"
        @checked-changed="changePlan"
      />
    </div>
    <RoundedCheckboxToggle @toggle-changed="monthlyYearlyToggle" />
  </div>
</template>

<style scoped></style>
