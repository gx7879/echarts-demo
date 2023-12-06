<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import { ref } from "vue";
import Echarts from "./components/Echarts.vue";
import carData from "./assets/mock/carJson.json";
import tabelData from "./assets/mock/tabelJson.json";
console.log(tabelData);
const BrakeWear_F_perc =
  tabelData.compredict_vehicle_health_mih_demo.BrakeWear_F_perc;
const BrakeWear_R_perc =
  tabelData.compredict_vehicle_health_mih_demo.BrakeWear_R_perc;
const data1 = [
  {
    name: "front pad wear",
    data: BrakeWear_F_perc[BrakeWear_F_perc.length - 1],
  },
  {
    name: "rear pad wear",
    data: BrakeWear_R_perc[BrakeWear_R_perc.length - 1],
  },
];
const options1 = ref({
  title: {
    text: "Pad wear",
  },
  tooltip: {
    trigger: "axis",
    valueFormatter: (value) => value + " %",
  },
  legend: {
    data: [data1[0].name, data1[1].name],
  },
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
      name: data1[0].name,
      type: "line",
      data: data1[0].data,
    },
    {
      name: data1[1].name,
      type: "line",
      data: data1[1].data,
    },
  ],
});
</script>

<template>
  <div class="text-center selection:bg-green-100">
    <div class="mx-auto grid max-w-[1000px] grid-cols-2 gap-10 px-4">
      <Echarts :options="options1"></Echarts>
      <Echarts :options="options1"></Echarts>
    </div>
  </div>
</template>

<style></style>
