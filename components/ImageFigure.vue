<template>
  <div
    class="grid grid-rows-[auto_40px] justify-content-center justify-items-center overflow-hidden"
  >
    <div>
      <img
        class="max-h-100 object-contain"
        :style="{
          width: width ? `${width}` : 'auto',
          height: height ? `${height}` : 'auto',
        }"
        :alt="caption"
        :src="resolveAssetUrl(src)"
      />
    </div>
    <div v-if="caption" class="text-xs">
      {{ caption }}
    </div>
  </div>
</template>

<script setup lang="ts">
import { resolveAssetUrl } from "../layoutHelper";

withDefaults(
  defineProps<{
    caption?: string;
    src: string;
    width?: string;
    height?: string;
  }>(),
  {},
);
</script>
