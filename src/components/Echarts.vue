<template>
  <div ref="chart" class="aspect-square w-full"></div>
</template>

<script setup>
import { ref, onMounted, markRaw, toRef, computed } from "vue";
import * as echarts from "echarts";
const props = defineProps({
  options: {
    type: Object,
  },
});
const echartInstance = ref(null);
const chart = ref(null);
const option = toRef(props.options);
const stack = option.value.stack ? { stack: "Total", areaStyle: {} } : {};
const max = option.value.yAxis?.max ? { max: option.value.yAxis.max } : {};
const xAxisData = option.value.dynamic ? {} : { data: option.value.xAxis.data };
const legend = option.value.dynamic
  ? { top: "7%", left: "3%" }
  : {
      data: option.value.data.map((data) => data.name),
      top: "7%",
      left: "3%",
    };
const dynamicData = option.value.dynamic
  ? [
      {
        name: option.value.title,
        type: "line",
        data: option.value.data,
        ...stack,
      },
    ]
  : [
      ...option.value.data.map((data) => ({
        name: data.name,
        type: "line",
        data: data.data,
        ...stack,
      })),
    ];
console.log(dynamicData);
const optionsVal = computed(() => ({
  title: {
    text: option.value.title,
    left: "3%",
  },
  tooltip: {
    trigger: "axis",
    valueFormatter: (value) => `${value} ${option.value.unit}`,
  },
  legend: legend,
  grid: {
    top: "20%",
    left: "3%",
    right: "4%",
    bottom: "3%",
    containLabel: true,
  },
  xAxis: {
    type: option.value.title === "Effect remaining range" ? "time" : "category",
    boundaryGap: false,
    ...xAxisData,
  },
  yAxis: {
    type: "value",
    axisLabel: {
      formatter: `{value} ${option.value.unit}`,
    },
    ...max,
  },
  series: [...dynamicData],
}));
if (option.value.title === "Effect remaining range") {
  console.log(optionsVal.value);
}
let now = new Date(1997, 9, 3);
let value = Math.random() * 1000;
let oneDay = 24 * 3600 * 1000;
function randomData() {
  now = new Date(+now + oneDay);
  value = value + Math.random() * 21 - 10;
  return {
    name: now.toString(),
    value: [
      [now.getFullYear(), now.getMonth() + 1, now.getDate()].join("/"),
      Math.round(value),
    ],
  };
}
function draw() {
  echartInstance.value.setOption(optionsVal.value);
  if (option.value.title === "Effect remaining range") {
    setInterval(function () {
      console.log(option.value);
      for (var i = 0; i < 5; i++) {
        const data = randomData();
        option.value.data.shift();
        option.value.data.push(data.value);
      }

      echartInstance.value.setOption({
        series: [
          {
            data: option.value.data,
          },
        ],
      });
    }, 1000);
  }
}
onMounted(() => {
  echartInstance.value = markRaw(echarts.init(chart.value));
  draw();
});
</script>

<style></style>
