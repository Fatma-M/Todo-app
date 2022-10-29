<template>
  <div class="toggle-wrapper">
    <label class="toggle">
      <input
        class="toggle-input"
        type="checkbox"
        :checked="mode === 'dark' ? 'checked' : false"
        @change="$emit('toggle')"
      />
      <img src="../assets/icon-moon.svg" v-if="mode === 'light'" />
      <img src="../assets/icon-sun.svg" v-else-if="mode === 'dark'" />
      <span class="toggler"></span>
    </label>
    <br />
  </div>
</template>

<script>
export default {
  props: ["mode"],
};
</script>
