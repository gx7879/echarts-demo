<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import { ref } from "vue";
import Echarts from "./components/Echarts.vue";
import carData from "./assets/mock/carJson.json";
import tabelData from "./assets/mock/tabelJson.json";
console.log(tabelData);
const options = ref({
  title: {
    text: "Stacked Line",
  },
  tooltip: {
    // trigger: "axis",
  },
  legend: {
    data: ["Email", "Union Ads"],
  },
  grid: {
    left: "3%",
    right: "4%",
    bottom: "3%",
    containLabel: true,
  },
  // toolbox: {
  //   feature: {
  //     saveAsImage: {},
  //   },
  // },
  xAxis: {
    type: "category",
    boundaryGap: false,
    data: ["current", "1000", "1500", "2000", "2500"],
  },
  yAxis: {
    type: "value",
    axisLabel: {
      formatter: "{value} %",
    },
  },
  series: [
    {
      name: "Email",
      type: "line",
      stack: "Total",
      data: [120, 132, 101, 134, 90, 230, 210],
    },
    {
      name: "Union Ads",
      type: "line",
      stack: "Total",
      data: [220, 182, 191, 234, 290, 330, 310],
    },
  ],
});
</script>

<template>
  <div class="text-center selection:bg-green-100">
    <div class="max-w-[1000px] px-4 grid grid-cols-2 gap-10 mx-auto">
      <Echarts :options="options"></Echarts>
    </div>
  </div>
</template>

<style></style>
