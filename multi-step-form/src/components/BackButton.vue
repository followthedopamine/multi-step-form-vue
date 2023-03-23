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
  <button @click="prevStep" class="ml-4" v-show="props.currentStep !== 1">Go back</button>
</template>

<style scoped></style>
