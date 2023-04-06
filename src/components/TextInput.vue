<script lang="ts" setup>
const props = defineProps({
  inputId: String,
  labelText: String,
  placeholder: String,
  inputText: String
})

const emit = defineEmits(['update:inputText'])

const updateInput = (event: Event) => {
  emit('update:inputText', (event.target as HTMLInputElement).value)
}
</script>

<template>
  <div>
    <label class="block text-marine-blue text-sm mb-1" :for="props.inputId">{{
      props.labelText
    }}</label>
    <input
      class="w-full font-medium border border-light-gray rounded p-2 pl-4 mb-4"
      type="text"
      :name="props.inputId"
      :id="props.inputId"
      :placeholder="props.placeholder"
      value=""
      @input="updateInput"
    />
  </div>
</template>
