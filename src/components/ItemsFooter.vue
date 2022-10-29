<template>
  <footer class="">
    <div class="counter">
      <span>{{ counter }} items left</span>
    </div>
    <div class="filter">
      <button
        :class="{ active: selectedFilter === 'all' }"
        @click="this.$emit('set', 'all'), setFilter('all')"
      >
        All
      </button>
      <button
        :class="{ active: selectedFilter === 'active' }"
        @click="this.$emit('set', 'active'), setFilter('active')"
        value="Active"
      >
        Active
      </button>
      <button
        :class="{ active: selectedFilter === 'completed' }"
        @click="this.$emit('set', 'checked'), setFilter('completed')"
      >
        Completed
      </button>
    </div>
    <div class="clear">
      <button @click="this.$emit('clearCompleted'), setFilter('all')">
        Clear Completed
      </button>
    </div>
  </footer>
</template>

<script>
export default {
  props: ["counter"],
  data() {
    return {
      selectedFilter: "all",
    };
  },

  computed: {},
  methods: {
    setFilter(tab) {
      this.selectedFilter = tab;
    },
  },
};
</script>
