<script setup lang="ts">
import Preview from "./Preview.vue";

defineProps<{
  ssr: boolean;
}>();
</script>

<template>
  <!-- <div class="tab-buttons">
    <button class="tab-button">
      <span>Preview</span>
    </button>
  </div> -->

  <div class="output-container">
    <Preview :show="true" :ssr="ssr" />
  </div>
</template>

<style scoped>
.output-container {
  height: calc(100% - var(--header-height));
  overflow: hidden;
  position: relative;
}

/* .tab-buttons {
  box-sizing: border-box;
  border-bottom: 1px solid var(--border);
  background-color: var(--bg);
  height: var(--header-height);
  overflow: hidden;
}
.tab-buttons button {
  padding: 0;
  box-sizing: border-box;
}
.tab-buttons span {
  font-size: 13px;
  font-family: var(--font-code);
  text-transform: uppercase;
  color: var(--text-light);
  display: inline-block;
  padding: 8px 16px 6px;
  line-height: 20px;
} */
/* button.active { */
/* .tab-button {
  color: var(--color-branding-dark);
  border-bottom: 3px solid var(--color-branding-dark);
} */
</style>
