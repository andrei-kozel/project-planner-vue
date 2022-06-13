<template>
  <div>
    <button
      class="btn-sm"
      :class="{ active: current === 'all' }"
      @click="updateFilter('all')"
    >
      all
    </button>
    <button
      class="btn-sm"
      :class="{ active: current === 'completed' }"
      @click="updateFilter('completed')"
    >
      completed
    </button>
    <button
      class="btn-sm"
      :class="{ active: current === 'ongoing' }"
      @click="updateFilter('ongoing')"
    >
      ongoing
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: ["current"],
  methods: {
    updateFilter(filter: string) {
      this.$emit("update", filter);
    },
  },
});
</script>

<style scoped>
.btn-sm {
  @apply hover:bg-gray-200 text-gray-600  px-2 mx-1 rounded-md;
}

.active {
  @apply hover:bg-green-400 bg-green-100 border-b-4 border-green-400;
}
</style>
