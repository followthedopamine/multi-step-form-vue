<script lang="ts" setup>
const props = defineProps({
  data: {
    type: Object,
    required: true
  },
  options: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['step2'])

const step2 = () => {
  emit('step2')
}
</script>

<template>
  <div id="step-4">
    <h1 class="text-marine-blue font-bold text-2xl mb-4">Finishing up</h1>
    <h2 class="h1 text-cool-gray mb-4">Double-check everything looks OK before confirming.</h2>
    <div class="bg-magnolia rounded p-4">
      <div class="flex text-marine-blue pb-3">
        <div>
          <div class="font-medium">
            {{ props.data.plan.display }} {{ !props.data.yearly ? '(Monthly)' : '(Yearly)' }}
          </div>
          <a
            class="text-cool-gray underline cursor-pointer hover:text-purplish-blue hover:decoration-2"
            @click="step2"
            >Change</a
          >
        </div>
        <div class="ml-auto font-bold flex items-end mb-2">
          <div>
            ${{
              !props.data.yearly
                ? props.data.plan.price + '/mo'
                : props.data.plan.price * 10 + '/ye'
            }}
          </div>
        </div>
      </div>
      <hr v-show="props.data.options.size" class="border-light-gray mb-2" />
      <ul>
        <li
          v-for="index in props.data.options"
          :key="'index' + index"
          class="flex py-1 text-cool-gray text-base"
        >
          <div>
            <div>{{ props.options[index].name }}</div>
          </div>
          <div class="ml-auto text-marine-blue">
            ${{
              !props.data.yearly
                ? props.options[index].price + '/mo'
                : props.options[index].price * 10 + '/ye'
            }}
          </div>
        </li>
      </ul>
    </div>

    <div class="p-4 flex">
      <div class="mt-0.5 text-cool-gray">
        Total {{ !props.data.yearly ? '(per month)' : '(per year)' }}
      </div>
      <div class="ml-auto text-purplish-blue font-bold text-lg">
        +${{ props.data.total }}/{{ !props.data.yearly ? 'mo' : 'yr' }}
      </div>
    </div>
  </div>
</template>

<style scoped></style>
