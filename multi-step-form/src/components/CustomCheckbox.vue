<script lang="ts" setup>
import { defineEmits, ref } from 'vue'

const props = defineProps({
  name: String,
  value: String
})

const emit = defineEmits(['toggleChecked'])

const isChecked = ref(false)

const handleChange = (event: Event) => {
  const target = event.target as HTMLInputElement
  isChecked.value = target.checked
  emit('toggleChecked', isChecked.value ? props.value : null)
}
</script>

<template>
  <div>
    <input
      type="checkbox"
      :id="props.name"
      :name="props.name"
      :value="props.value"
      @change="handleChange"
      class="opacity-0 absolute h-8 w-8"
    />
    <div
      class="bg-white border rounded-md border-light-gray w-6 h-6 flex flex-shrink-0 justify-center items-center mr-2 focus-within:border-pastel-blue"
    >
      <svg
        class="fill-current hidden w-3 h-3 text-blue-600 pointer-events-none"
        version="1.1"
        viewBox="0 0 17 12"
        xmlns="http://www.w3.org/2000/svg"
      >
        <g fill="none" fill-rule="evenodd">
          <g transform="translate(-9 -11)" fill="#FFFFFF" fill-rule="nonzero">
            <path
              d="m25.576 11.414c0.56558 0.55188 0.56558 1.4439 0 1.9961l-9.404 9.176c-0.28213 0.27529-0.65247 0.41385-1.0228 0.41385-0.37034 0-0.74068-0.13855-1.0228-0.41385l-4.7019-4.588c-0.56584-0.55188-0.56584-1.4442 0-1.9961 0.56558-0.55214 1.4798-0.55214 2.0456 0l3.679 3.5899 8.3812-8.1779c0.56558-0.55214 1.4798-0.55214 2.0456 0z"
            />
          </g>
        </g>
      </svg>
    </div>
  </div>
</template>

<style scoped>
input:checked + div {
  @apply bg-purplish-blue;
  @apply border-purplish-blue;
}
input:checked + div svg {
  @apply block;
}
</style>
