<template>
  <header>
    <nav>
      <h1>todo</h1>
      <toggle-mode :mode="mode" @toggle="$emit('toggle')"> </toggle-mode>
    </nav>
  </header>
</template>

<script>
import ToggleMode from "./ToggleMode";

export default {
  components: { ToggleMode },

  props: ["mode"],
};
</script>
