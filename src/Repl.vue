<script setup lang="ts">
import SplitPane from "./SplitPane.vue";
import Editor from "./editor/Editor.vue";
import Output from "./output/Output.vue";
import { Store, ReplStore, SFCOptions } from "./store";
import { provide, toRef } from "vue";

export interface Props {
  store?: Store;
  autoResize?: boolean;
  showImportMap?: boolean;
  clearConsole?: boolean;
  sfcOptions?: SFCOptions;
  layout?: string;
  ssr?: boolean;
}

const props = withDefaults(defineProps<Props>(), {
  store: () => new ReplStore(),
  autoResize: true,
  showImportMap: true,
  clearConsole: true,
  ssr: false,
});

props.store.options = props.sfcOptions;
props.store.init();

provide("store", props.store);
provide("autoresize", props.autoResize);
provide("import-map", toRef(props, "showImportMap"));
provide("clear-console", toRef(props, "clearConsole"));
</script>

<template>
  <div class="vue-repl">
    <SplitPane :layout="layout">
      <template #top>
        <Output :ssr="!!props.ssr" />
      </template>
      <template #bottom>
        <Editor />
      </template>
    </SplitPane>
  </div>
</template>

<style scoped>
.vue-repl {
  --bg: #fff;
  --bg-soft: #f8f8f8;
  --border: #ddd;
  --text-light: #888;
  --font-code: Menlo, Monaco, Consolas, "Courier New", monospace;
  --color-branding: #42b883;
  --color-branding-dark: #416f9c;
  --header-height: 38px;

  font-size: 13px;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  margin: 0;
  overflow: hidden;
  background-color: var(--bg-soft);
}

.dark .vue-repl {
  --bg: #1a1a1a;
  --bg-soft: #242424;
  --border: #383838;
  --text-light: #aaa;
  --color-branding: #42d392;
  --color-branding-dark: #89ddff;
}

:deep(button) {
  border: none;
  outline: none;
  cursor: pointer;
  margin: 0;
  background-color: transparent;
}
</style>
