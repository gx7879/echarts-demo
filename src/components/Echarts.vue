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
const optionsVal = computed(() => ({
  title: {
    text: option.value.title,
    left: "3%",
  },
  tooltip: {
    trigger: "axis",
    valueFormatter: (value) => `${value} ${option.value.unit}`,
  },
  legend: {
    data: option.value.data.map((data) => data.name),
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
    data: option.value.xAxis.data,
  },
  yAxis: {
    type: "value",
    axisLabel: {
      formatter: `{value} ${option.value.unit}`,
    },
    ...max,
  },
  series: [
    ...option.value.data.map((data) => ({
      name: data.name,
      type: "line",
      data: data.data,
      ...stack,
    })),
  ],
}));
let now = new Date(1997, 9, 3);
let value = Math.random() * 1000;
function randomData() {
  let oneDay = 24 * 3600 * 1000;
  now = new Date(+now + oneDay);
  value = value + Math.random() * 21 - 10;
  return {
    time: [now.getFullYear(), now.getMonth() + 1, now.getDate()].join("/"),
    value,
  };
}
function draw() {
  echartInstance.value.setOption(optionsVal.value);
  if (option.value.title === "Effect remaining range") {
    setInterval(function () {
      // console.log(123);
      for (var i = 0; i < 5; i++) {
        const data = randomData();
        if (option.value.xAxis.data.length >= 5) {
          option.value.xAxis.data.shift();
          option.value.data[0].data.shift();
        }
        option.value.xAxis.data.push(data.time);
        option.value.data[0].data.push(data.value);
      }

      echartInstance.value.setOption({
        xAxis: { data: optionsVal.value.xAxis.data },
        series: [
          {
            data: optionsVal.value.series[0].data,
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
