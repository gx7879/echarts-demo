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
const option = props.options;
const stack = option.stack ? { stack: "Total", areaStyle: {} } : {};
const max = option.yAxis?.max ? { max: option.yAxis.max } : {};
const optionsVal = ref({
  title: {
    text: option.title,
    left: "3%",
  },
  tooltip: {
    trigger: "axis",
    valueFormatter: (value) => `${value} ${option.unit}`,
  },
  legend: {
    data: option.data.map((data) => data.name),
    top: "7%",
    left: "3%",
  },
  grid: {
    top: "20%",
    left: "3%",
    right: "4%",
    bottom: "3%",
    containLabel: true,
  },
  xAxis: {
    type: "category",
    boundaryGap: false,
    data: option.xAxis.data,
  },
  yAxis: {
    type: "value",
    axisLabel: {
      formatter: `{value} ${option.unit}`,
    },
    ...max,
  },
  series: [
    ...option.data.map((data) => ({
      name: data.name,
      type: "line",
      data: data.data,
      ...stack,
    })),
  ],
});
console.log(optionsVal.value);
function draw() {
  echartInstance.value.setOption(optionsVal.value);
}
onMounted(() => {
  echartInstance.value = markRaw(echarts.init(chart.value));
  draw();
});
</script>

<style></style>
