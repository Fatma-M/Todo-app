<template>
  <div class="app" :class="mode">
    <the-header :mode="mode" @toggle="toggleMode"></the-header>
    <items-list></items-list>
  </div>
</template>

<script>
import TheHeader from "./components/TheHeader.vue";
import ItemsList from "./components/ItemsList.vue";

export default {
  components: { TheHeader, ItemsList },
  data() {
    return {
      mode: "light",
    };
  },

  methods: {
    toggleMode() {
      if (this.mode === "light") {
        this.mode = "dark";
      } else {
        this.mode = "light";
      }
    },
  },
};
</script>

<style>
/*  */
</style>
