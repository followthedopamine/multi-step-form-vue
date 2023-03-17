<script lang="ts" setup></script>

<template>
  <div class="radios">
    <input id="arcade" name="arcade" type="radio" class="w-0 fixed opacity-0" />
    <label class="w-full border border-light-gray rounded-lg h-20 flex items-center" for="arcade">
      <i class="arcade w-[40px] h-[40px] block mx-4"></i>
      Arcade
    </label>
  </div>
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
