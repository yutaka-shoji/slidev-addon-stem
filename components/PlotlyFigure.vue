<script setup lang="ts">
import { onMounted, watch, ref, computed, onBeforeUnmount } from "vue";
import { newPlot, react } from "plotly.js-dist-min";

const props = defineProps<{
  src: string;
  caption: string;
  width?: string;
  height?: string;
  fontSize?: number;
}>();

const plotDiv = ref<HTMLElement>();
const figure = ref<any>(null);
const resizeObserver = ref<ResizeObserver | null>(null);

// set container style
const containerStyle = computed(() => ({
  width: props.width || "100%",
  height: props.height || "360px",
}));

// get current font family
const getCurrentFontFamily = () => {
  const body = document.body;
  return window.getComputedStyle(body).fontFamily;
};

// update plot config
const updatePlotConfig = (data: any, container: HTMLElement) => {
  const fontFamily = getCurrentFontFamily();

  // update layout
  const layout = {
    ...data.layout,
    width: container.clientWidth,
    height: container.clientHeight,
    autosize: false,
    font: {
      ...data.layout?.font,
      family: fontFamily,
      size: props.fontSize,
    },
    xaxis: {
      ...data.layout?.xaxis,
      tickfont: {
        ...data.layout?.xaxis?.tickfont,
        size: props.fontSize,
      },
    },
    yaxis: {
      ...data.layout?.yaxis,
      tickfont: {
        ...data.layout?.yaxis?.tickfont,
        size: props.fontSize,
      },
    },
  };

  return {
    data: data.data,
    layout,
  };
};

// update plot size
const updatePlotSize = () => {
  if (!plotDiv.value || !figure.value) return;

  const container = plotDiv.value;
  const updatedFigure = updatePlotConfig(figure.value, container);

  try {
    react(container, updatedFigure.data, updatedFigure.layout, {
      responsive: true,
    });
  } catch (error) {
    console.error("Error updating plot size:", error);
  }
};

// initialize plot
const initPlot = async () => {
  try {
    const container = plotDiv.value;
    if (!container) return;

    const response = await fetch(props.src);
    const data = await response.json();
    figure.value = updatePlotConfig(data, container);

    await newPlot(container, figure.value.data, figure.value.layout, {
      responsive: true,
    });

    // observe resize
    if (resizeObserver.value) {
      resizeObserver.value.disconnect();
    }
    resizeObserver.value = new ResizeObserver(updatePlotSize);
    resizeObserver.value.observe(container);
  } catch (error) {
    console.error("Error loading plot:", error);
  }
};

// watch props
watch(() => props.src, initPlot);
watch([() => props.fontSize], () => {
  if (figure.value && plotDiv.value) {
    const updatedFigure = updatePlotConfig(figure.value, plotDiv.value);
    react(plotDiv.value, updatedFigure.data, updatedFigure.layout, {
      responsive: true,
    });
  }
});

// unmount
onBeforeUnmount(() => {
  if (resizeObserver.value) {
    resizeObserver.value.disconnect();
  }
});

onMounted(initPlot);
</script>

<template>
  <div class="w-full">
    <div
      class="mx-auto"
      :style="[containerStyle, { margin: '0 auto' }]"
      ref="plotDiv"
    ></div>
    <div v-if="caption" class="text-xs text-center mt-2">
      {{ caption }}
    </div>
  </div>
</template>
