<script lang="ts" setup>
import TextInput from './TextInput.vue'

const props = defineProps({ errors: { type: Object, required: true } })
const emit = defineEmits(['updateName', 'updateEmail', 'updatePhone'])

const updateName = (name: string) => {
  emit('updateName', name)
}

const updateEmail = (email: string) => {
  emit('updateEmail', email)
}

const updatePhone = (phone: string) => {
  emit('updatePhone', phone)
}
</script>

<template>
  <div id="step-1">
    <h1 class="text-marine-blue font-bold text-2xl mb-4">Personal info</h1>
    <h2 class="h1 text-cool-gray mb-4">
      Please provide your name, email address, and phone number.
    </h2>

    <TextInput
      input-id="name"
      label-text="Name"
      placeholder="e.g. Stephen King"
      @update:input-text="updateName"
      :error="props.errors.name"
    />
    <TextInput
      input-id="email"
      label-text="Email Address"
      placeholder="e.g. stephenking@lorem.com"
      @update:input-text="updateEmail"
      :error="props.errors.email"
    />
    <TextInput
      input-id="phone"
      label-text="Phone Number"
      placeholder="e.g. +1 234 567 890"
      @update:input-text="updatePhone"
      :error="props.errors.phone"
    />
  </div>
</template>

<style scoped></style>
