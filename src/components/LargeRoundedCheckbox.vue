<script lang="ts" setup>
import CustomCheckbox from './CustomCheckbox.vue'
import { defineProps, ref } from 'vue'

const props = defineProps({
  name: String,
  value: String,
  label: String,
  text: String,
  price: String,
  index: Number
})

const emit = defineEmits(['toggleChecked'])

const isChecked = ref(false)

const toggleChecked = (checked: boolean) => {
  isChecked.value = checked
  emit('toggleChecked', isChecked.value ? props.value : null, props.index)
}
</script>

<template>
  <div class="checkbox">
    <CustomCheckbox
      class="absolute m-4 mt-7"
      :name="props.name"
      :value="props.value"
      @toggle-checked="toggleChecked"
    />
    <label
      :for="props.name"
      class="cursor-pointer flex items-center w-full border border-light-gray hover:border-[#544c97] rounded-lg h-[4.5rem] mb-4 bg-magnolia"
      :class="{
        'border-light-gray': !isChecked,
        'border-purplish-blue': isChecked,
        'bg-opacity-0': !isChecked
      }"
    >
      <label :for="props.name" class="cursor-pointer ml-14 h-full w-full">
        <div class="h-full w-full flex items-center">
          <div class="-mt-2">
            <div class="text-marine-blue font-medium text-[1.05rem] tracking-tight">
              {{ props.label }}
            </div>
            <div class="text-cool-gray text-xs text-[0.87rem] tracking-tight">
              {{ props.text }}
            </div>
          </div>
          <div class="text-purplish-blue text-sm h-full ml-auto">
            <div class="flex self-end items-center h-full font-medium pr-3">
              <div>{{ props.price }}</div>
            </div>
          </div>
        </div>
      </label>
    </label>
  </div>
</template>

<style scoped>
.checkbox input[type='checkbox']:checked + label {
  border-color: #544c97;
  background-color: #f8f9fe;
}
</style>

<!-- <div>
            <input
              id="online-service"
              type="checkbox"
              class="accent-purplish-blue w-5 h-5 m-4 cursor-pointer absolute mt-7"
            />
            <label
              for="online-service"
              class="cursor-pointer flex items-center w-full border border-light-gray rounded-lg h-20 mb-4"
            >
              <label for="online-service" class="cursor-pointer ml-14 h-full">
                <div class="h-full flex items-center">
                  <div class="w-11/12 float-left -mt-2">
                    <div class="text-marine-blue font-medium text-lg text-[1.05rem] tracking-tight">
                      Online service
                    </div>
                    <div class="text-cool-gray text-xs tracking-tight w-11/12">
                      Access to multiplayer games
                    </div>
                  </div>
                  <div class="w-1/12 float-right text-purplish-blue text-sm h-full">
                    <div class="flex items-center h-full -ml-3 font-medium"><div>+$1/mo</div></div>
                  </div>
                </div>
              </label>
            </label>
          </div> -->
