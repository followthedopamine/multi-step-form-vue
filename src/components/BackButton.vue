<script lang="ts" setup>
const props = defineProps({
  currentStep: Number
})

const emit = defineEmits(['prevStep'])

const prevStep = () => {
  emit('prevStep')
}
</script>

<template>
  <button
    @click="prevStep"
    class="ml-4 text-cool-gray hover:text-purplish-blue hover:underline hover:decoration-2"
    v-show="props.currentStep !== 1"
  >
    Go Back
  </button>
</template>

<style scoped></style>
