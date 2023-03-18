<script lang="ts" setup></script>

<template>
  <div class="bg-magnolia flex justify-around p-3 px-14 font-medium rounded-lg mt-6">
    <input id="yearly" type="checkbox" hidden />
    <label for="yearly" class="unchk-label text-marine-blue"> Monthly </label>
    <label for="yearly" class="relative inline-flex items-center cursor-pointer group">
      <div class="w-11 h-6 bg-marine-blue rounded-full">
        <div
          class="absolute top-[4px] left-[4px] bg-white rounded-full h-4 w-4 transition-all check-toggle"
        ></div>
      </div>
    </label>

    <label for="yearly" class="chk-label text-marine-blue"> Yearly </label>
  </div>
</template>

<style scoped>
input[type='checkbox']:not(:checked) ~ .chk-label {
  @apply text-cool-gray;
}

input[type='checkbox']:checked ~ .unchk-label {
  @apply text-cool-gray;
}

input[type='checkbox']:checked ~ label .check-toggle {
  transform: translateX(20px);
}
</style>

<!-- <div class="bg-magnolia flex justify-around p-3 px-14 font-medium">
  <label for="yearly" class="relative inline-flex items-center cursor-pointer">
    <input id="yearly" type="checkbox" value="yearly" class="sr-only peer chk" />
    <label class="chk-label" for="yearly">Monthly</label>
    <div
      class="w-11 h-6 bg-marine-blue peer-focus:outline-none peer-focus:ring-4 rounded-full peer peer-checked:after:translate-x-5 after:content-[''] after:absolute after:top-[4px] after:left-[4px] after:bg-white after:rounded-full after:h-4 after:w-4 after:transition-all "
    ></div>
  </label>
  <label class="unchk-label" for="yearly">Yearly</label>
</div> -->
