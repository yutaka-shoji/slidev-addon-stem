<template>
  <div class="slidev-layout default">
    <div>
      <slot name="header" />
    </div>
    <div grid gap-4 grid-cols-2 mt-4 h-100>
      <div overflow-auto>
        <slot name="content" />
      </div>
      <div>
        <ImageFigure :caption="figureCaption" :src="figureUrl" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
withDefaults(
  defineProps<{
    figureCaption?: string;
    figureUrl: string;
  }>(),
  {},
);
</script>
