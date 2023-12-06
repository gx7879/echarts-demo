<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import { ref } from "vue";
import dayjs from "dayjs";
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
    data: data1.map((data) => data.name),
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
    max: 100,
  },
  series: [
    ...data1.map((data) => ({
      name: data.name,
      type: "line",
      data: data.data,
    })),
  ],
});
const time = carData.Timestamp.map((time) => dayjs(time).format("HH:mm"));
const MassEstim = carData.compredict_mass_mih_demo.Payload;
const data2 = [
  {
    name: "Truck weight",
    data: Array(MassEstim.length).fill(2500),
  },
  {
    name: "Payload",
    data: MassEstim,
  },
];
const options2 = ref({
  title: {
    text: "Vehicle mess",
  },
  tooltip: {
    trigger: "axis",
    valueFormatter: (value) => value + " kg",
  },
  legend: {
    data: data2.map((data) => data.name),
  },
  grid: {
    left: "3%",
    right: "4%",
    bottom: "3%",
    containLabel: true,
  },
  xAxis: {
    type: "category",
    boundaryGap: false,
    data: time,
  },
  yAxis: {
    type: "value",
    axisLabel: {
      formatter: "{value} kg",
    },
  },
  series: [
    {
      name: data2[0].name,
      type: "line",
      stack: "Total",
      areaStyle: {},
      data: data2[0].data,
    },
    {
      name: data2[1].name,
      type: "line",
      stack: "Total",
      areaStyle: {},
      data: data2[1].data,
    },
  ],
});
const TireWear_Fl_perc =
  tabelData.compredict_vehicle_health_mih_demo.TireWear_Fl_perc;
const TireWear_Fr_perc =
  tabelData.compredict_vehicle_health_mih_demo.TireWear_Fr_perc;
const TireWear_Rl_perc =
  tabelData.compredict_vehicle_health_mih_demo.TireWear_Rl_perc;
const TireWear_Rr_perc =
  tabelData.compredict_vehicle_health_mih_demo.TireWear_Rr_perc;
const data3 = [
  {
    name: "front left tire wear",
    data: TireWear_Fl_perc[TireWear_Fl_perc.length - 1],
  },
  {
    name: "front right tire wear",
    data: TireWear_Fr_perc[TireWear_Fr_perc.length - 1],
  },
  {
    name: "Rear left tire wear",
    data: TireWear_Rl_perc[TireWear_Rl_perc.length - 1],
  },
  {
    name: "Rear right tire wear",
    data: TireWear_Rr_perc[TireWear_Rr_perc.length - 1],
  },
];
const options3 = ref({
  title: {
    text: "Tire wear",
  },
  tooltip: {
    trigger: "axis",
    valueFormatter: (value) => value + " %",
  },
  legend: {
    data: data3.map((data) => data.name),
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
    max: 100,
  },
  series: [
    ...data3.map((data) => ({
      name: data.name,
      type: "line",
      data: data.data,
    })),
  ],
});

const data4 = [
  {
    name: "Effect remaining range",
    data: carData.compredict_mass_mih_demo.remRange_effective,
  },
];
const options4 = ref({
  title: {
    text: "Effect remaining range",
  },
  tooltip: {
    trigger: "axis",
    valueFormatter: (value) => value + " km",
  },
  legend: {
    data: data4.map((data) => data.name),
  },
  grid: {
    left: "3%",
    right: "4%",
    bottom: "3%",
    containLabel: true,
  },
  xAxis: {
    type: "category",
    boundaryGap: false,
    data: time,
  },
  yAxis: {
    type: "value",
    axisLabel: {
      formatter: "{value} km",
    },
  },
  series: [
    {
      name: data4[0].name,
      type: "line",
      data: data4[0].data,
    },
  ],
});
const HvBatWear_perc =
  tabelData.compredict_vehicle_health_mih_demo.HvBatWear_perc;
const data5 = [
  {
    name: "Battery",
    data: HvBatWear_perc[HvBatWear_perc.length - 1],
  },
];
const options5 = ref({
  title: {
    text: "Battery",
  },
  tooltip: {
    trigger: "axis",
    valueFormatter: (value) => value + " %",
  },
  legend: {
    data: data5.map((data) => data.name),
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
    max: 100,
  },
  series: [
    ...data5.map((data) => ({
      name: data.name,
      type: "line",
      data: data.data,
    })),
  ],
});
</script>

<template>
  <div class="text-center selection:bg-green-100">
    <div class="mx-auto grid max-w-[1000px] grid-cols-2 gap-10 px-4">
      <Echarts :options="options1"></Echarts>
      <Echarts :options="options2"></Echarts>
      <Echarts :options="options3"></Echarts>
      <Echarts :options="options4"></Echarts>
      <Echarts :options="options5"></Echarts>
    </div>
  </div>
</template>

<style></style>
