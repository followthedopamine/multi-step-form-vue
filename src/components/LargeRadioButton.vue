<script lang="ts" setup>
const props = defineProps({
  value: String,
  label: String,
  text: String,
  subText: String,
  name: String,
  index: Number,
  checked: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['checkedChanged'])

const handleChange = () => {
  emit('checkedChanged', props.checked, props.index)
}
</script>

<template>
  <input
    :id="props.value"
    :name="props.name"
    type="radio"
    class="w-0 fixed opacity-0"
    :checked="props.checked"
    @change="handleChange"
  />
  <label
    class="cursor-pointer w-full border border-light-gray rounded-lg h-20 flex items-center mb-4"
    :for="props.value"
  >
    <i class="w-[40px] h-[40px] block mx-4" :class="props.value"></i>
    <div>
      <div class="text-marine-blue font-medium text-lg">{{ props.label }}</div>
      <div class="text-cool-gray">{{ props.text }}</div>
      <div class="text-marine-blue text-sm">{{ props.subText }}</div>
    </div>
  </label>
</template>

<style scoped>
.arcade {
  background-image: url('../assets/images/icon-arcade.svg');
}

.advanced {
  background-image: url('../assets/images/icon-advanced.svg');
}

.pro {
  background-image: url('../assets/images/icon-pro.svg');
}

.radios input[type='radio']:checked + label {
  border-color: #544c97;
  background-color: #f8f9fe;
}
</style>
