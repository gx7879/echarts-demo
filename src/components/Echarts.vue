<template>
  <div ref="chart" class="aspect-square w-full"></div>
</template>

<script setup>
import { ref, onMounted, markRaw } from "vue";
import * as echarts from "echarts";
const props = defineProps({
  options: {
    type: Object,
  },
});
const echartInstance = ref(null);
const chart = ref(null);
function draw() {
  const option = props.options;
  echartInstance.value.setOption(option);
}
onMounted(() => {
  echartInstance.value = markRaw(echarts.init(chart.value));
  draw();
});
</script>

<style>
</style>