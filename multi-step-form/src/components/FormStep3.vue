<script lang="ts" setup>
import LargeRoundedCheckbox from './LargeRoundedCheckbox.vue'

const props = defineProps({
  data: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['toggleCheckedCheckbox'])

const toggleCheckedCheckbox = (checked: Boolean, index: number) => {
  emit('toggleCheckedCheckbox', checked, index)
}
</script>

<template>
  <div id="step-3">
    <h1 class="text-marine-blue font-bold text-2xl mb-4">Pick add-ons</h1>
    <h2 class="h1 text-cool-gray mb-4">Add-ons help enhance your gaming experience.</h2>
    <div class="checkboxes">
      <LargeRoundedCheckbox
        name="online-service"
        value="online"
        label="Online service"
        text="Access to multiplayer games"
        :price="props.data.yearly ? '+$10/yr' : '+$1/mo'"
        :index="0"
        @toggle-checked="toggleCheckedCheckbox"
      />
      <LargeRoundedCheckbox
        name="larger-storage"
        value="larger"
        label="Larger storage"
        text="Extra 1TB of cloud save"
        :price="props.data.yearly ? '+$20/yr' : '+$2/mo'"
        :index="1"
        @toggle-checked="toggleCheckedCheckbox"
      />
      <LargeRoundedCheckbox
        name="customizable-profile"
        value="profile"
        label="Customizable profile"
        text="Custom theme on your profile"
        :price="props.data.yearly ? '+$20/yr' : '+$2/mo'"
        :index="2"
        @toggle-checked="toggleCheckedCheckbox"
      />
    </div>
  </div>
</template>

<style scoped></style>
