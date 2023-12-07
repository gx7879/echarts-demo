<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import { ref } from "vue";
import dayjs from "dayjs";
import Echarts from "./components/Echarts.vue";
import carData from "./assets/mock/carJson.json";
import tabelData from "./assets/mock/tabelJson.json";

const time = carData.Timestamp.map((time) => dayjs(time).format("HH:mm"));
const echartData = [
  {
    index: 1,
    title: "Pad wear",
    unit: "%",
    xAxis: {
      data: ["current", "1000", "1500", "2000", "2500"],
    },
    yAxis: {
      max: 100,
    },
    data: [
      {
        name: "front pad wear",
        data: [53.4, 52.1, 50.8, 50.3, 50],
      },
      {
        name: "rear pad wear",
        data: [47.4, 46, 44.7, 43.5, 42.1],
      },
    ],
  },
  {
    index: 2,
    title: "Vehicle mess",
    unit: "kg",
    xAxis: {
      data: time,
    },
    data: [
      {
        name: "Truck weight",
        data: Array(3).fill(2500),
      },
      {
        name: "Payload",
        data: [1000, 1100, 1200],
      },
    ],
    stack: true,
  },
  {
    index: 3,
    title: "Tire wear",
    unit: "%",
    xAxis: {
      data: ["current", "1000", "1500", "2000", "2500"],
    },
    yAxis: {
      max: 100,
    },
    data: [
      {
        name: "front left tire wear",
        data: [34.1, 27.6, 24.1, 20.8, 17.5],
      },
      {
        name: "front right tire wear",
        data: [34.5, 29.8, 26.8, 23.5, 20.3],
      },
      {
        name: "Rear left tire wear",
        data: [20.3, 13.5, 9.9, 6.3, 3.5],
      },
      {
        name: "Rear right tire wear",
        data: [21.7, 15.9, 12.6, 8.9, 5.5],
      },
    ],
  },
  {
    index: 4,
    title: "Effect remaining range",
    unit: "km",
    xAxis: {
      data: time,
    },
    data: [
      {
        name: "Effect remaining range",
        data: [185, 187, 189],
      },
    ],
  },
  {
    index: 5,
    title: "Battery",
    unit: "%",
    xAxis: {
      data: ["current", "1000", "1500", "2000", "2500"],
    },
    yAxis: {
      max: 100,
    },
    data: [
      {
        name: "Battery",
        data: [76.8, 76.6, 76.2, 75.7, 75.1],
      },
    ],
  },
  {
    index: 6,
    title: "Speed",
    unit: "km",
    xAxis: {
      data: time,
    },
    yAxis: {
      max: 200,
    },
    data: [
      {
        name: "Speed",
        data: [20, 50, 70],
      },
    ],
  },
  {
    index: 8,
    title: "Coaching",
    unit: "%",
    xAxis: {
      data: time,
    },
    yAxis: {
      max: 100,
    },
    data: [
      {
        name: "Acceleration",
        data: [92, 91, 90],
      },
      {
        name: "Braking",
        data: [98, 97, 96],
      },
      {
        name: "Cornering",
        data: [91, 90, 89],
      },
    ],
  },
  {
    index: 7,
    title: "SOC",
    unit: "%",
    xAxis: {
      data: time,
    },
    yAxis: {
      max: 100,
    },
    data: [
      {
        name: "SOC",
        data: [73, 72, 71],
      },
    ],
  },
].sort((a, b) => a.index - b.index);
// const BrakeWear_F_perc =
//   tabelData.compredict_vehicle_health_mih_demo.BrakeWear_F_perc;
// const BrakeWear_R_perc =
//   tabelData.compredict_vehicle_health_mih_demo.BrakeWear_R_perc;
// const data1 = [
//   {
//     name: "front pad wear",
//     data: BrakeWear_F_perc[BrakeWear_F_perc.length - 1],
//   },
//   {
//     name: "rear pad wear",
//     data: BrakeWear_R_perc[BrakeWear_R_perc.length - 1],
//   },
// ];
// const options1 = ref({
//   title: {
//     text: "Pad wear",
//     left: "3%",
//   },
//   tooltip: {
//     trigger: "axis",
//     valueFormatter: (value) => value + " %",
//   },
//   legend: {
//     data: data1.map((data) => data.name),
//     top: "7%",
//     left: "3%",
//   },
//   grid: {
//     top: "20%",
//     left: "3%",
//     right: "4%",
//     bottom: "3%",
//     containLabel: true,
//   },
//   xAxis: {
//     type: "category",
//     boundaryGap: false,
//     data: ["current", "1000", "1500", "2000", "2500"],
//   },
//   yAxis: {
//     type: "value",
//     axisLabel: {
//       formatter: "{value} %",
//     },
//     max: 100,
//   },
//   series: [
//     ...data1.map((data) => ({
//       name: data.name,
//       type: "line",
//       data: data.data,
//     })),
//   ],
// });
// const MassEstim = carData.compredict_mass_mih_demo.Payload;
// const data2 = [
//   {
//     name: "Truck weight",
//     data: Array(MassEstim.length).fill(2500),
//   },
//   {
//     name: "Payload",
//     data: MassEstim,
//   },
// ];
// const options2 = ref({
//   title: {
//     text: "Vehicle mess",
//     left: "3%",
//   },
//   tooltip: {
//     trigger: "axis",
//     valueFormatter: (value) => value + " kg",
//   },
//   legend: {
//     data: data2.map((data) => data.name),
//     top: "7%",
//     left: "3%",
//   },
//   grid: {
//     top: "20%",
//     left: "3%",
//     right: "4%",
//     bottom: "3%",
//     containLabel: true,
//   },
//   xAxis: {
//     type: "category",
//     boundaryGap: false,
//     data: time,
//   },
//   yAxis: {
//     type: "value",
//     axisLabel: {
//       formatter: "{value} kg",
//     },
//   },
//   series: [
//     ...data2.map((data) => ({
//       name: data.name,
//       type: "line",
//       stack: "Total",
//       areaStyle: {},
//       data: data.data,
//     })),
//   ],
// });
// const TireWear_Fl_perc =
//   tabelData.compredict_vehicle_health_mih_demo.TireWear_Fl_perc;
// const TireWear_Fr_perc =
//   tabelData.compredict_vehicle_health_mih_demo.TireWear_Fr_perc;
// const TireWear_Rl_perc =
//   tabelData.compredict_vehicle_health_mih_demo.TireWear_Rl_perc;
// const TireWear_Rr_perc =
//   tabelData.compredict_vehicle_health_mih_demo.TireWear_Rr_perc;
// const data3 = [
//   {
//     name: "front left tire wear",
//     data: TireWear_Fl_perc[TireWear_Fl_perc.length - 1],
//   },
//   {
//     name: "front right tire wear",
//     data: TireWear_Fr_perc[TireWear_Fr_perc.length - 1],
//   },
//   {
//     name: "Rear left tire wear",
//     data: TireWear_Rl_perc[TireWear_Rl_perc.length - 1],
//   },
//   {
//     name: "Rear right tire wear",
//     data: TireWear_Rr_perc[TireWear_Rr_perc.length - 1],
//   },
// ];
// const options3 = ref({
//   title: {
//     text: "Tire wear",
//     left: "3%",
//   },
//   tooltip: {
//     trigger: "axis",
//     valueFormatter: (value) => value + " %",
//   },
//   legend: {
//     data: data3.map((data) => data.name),
//     top: "7%",
//     left: "3%",
//   },
//   grid: {
//     top: "20%",
//     left: "3%",
//     right: "4%",
//     bottom: "3%",
//     containLabel: true,
//   },
//   xAxis: {
//     type: "category",
//     boundaryGap: false,
//     data: ["current", "1000", "1500", "2000", "2500"],
//   },
//   yAxis: {
//     type: "value",
//     axisLabel: {
//       formatter: "{value} %",
//     },
//     max: 100,
//   },
//   series: [
//     ...data3.map((data) => ({
//       name: data.name,
//       type: "line",
//       data: data.data,
//     })),
//   ],
// });

// const data4 = [
//   {
//     name: "Effect remaining range",
//     data: carData.compredict_mass_mih_demo.remRange_effective,
//   },
// ];
// const options4 = ref({
//   title: {
//     text: "Effect remaining range",
//     left: "3%",
//   },
//   tooltip: {
//     trigger: "axis",
//     valueFormatter: (value) => value + " km",
//   },
//   legend: {
//     data: data4.map((data) => data.name),
//     top: "7%",
//     left: "3%",
//   },
//   grid: {
//     top: "20%",
//     left: "3%",
//     right: "4%",
//     bottom: "3%",
//     containLabel: true,
//   },
//   xAxis: {
//     type: "category",
//     boundaryGap: false,
//     data: time,
//   },
//   yAxis: {
//     type: "value",
//     axisLabel: {
//       formatter: "{value} km",
//     },
//   },
//   series: [
//     ...data4.map((data) => ({
//       name: data.name,
//       type: "line",
//       data: data.data,
//     })),
//   ],
// });
// const HvBatWear_perc =
//   tabelData.compredict_vehicle_health_mih_demo.HvBatWear_perc;
// const data5 = [
//   {
//     name: "Battery",
//     data: HvBatWear_perc[HvBatWear_perc.length - 1],
//   },
// ];
// const options5 = ref({
//   title: {
//     text: "Battery",
//     left: "3%",
//   },
//   tooltip: {
//     trigger: "axis",
//     valueFormatter: (value) => value + " %",
//   },
//   legend: {
//     data: data5.map((data) => data.name),
//     top: "7%",
//     left: "3%",
//   },
//   grid: {
//     top: "20%",
//     left: "3%",
//     right: "4%",
//     bottom: "3%",
//     containLabel: true,
//   },
//   xAxis: {
//     type: "category",
//     boundaryGap: false,
//     data: ["current", "1000", "1500", "2000", "2500"],
//   },
//   yAxis: {
//     type: "value",
//     axisLabel: {
//       formatter: "{value} %",
//     },
//     max: 100,
//   },
//   series: [
//     ...data5.map((data) => ({
//       name: data.name,
//       type: "line",
//       data: data.data,
//     })),
//   ],
// });
// const data6 = [{ name: "Speed", data: carData.compredict_mass_mih_demo.speed }];
// const options6 = ref({
//   title: {
//     text: "Speed",
//     left: "3%",
//   },
//   tooltip: {
//     trigger: "axis",
//     valueFormatter: (value) => value + " km",
//   },
//   legend: {
//     data: data6.map((data) => data.name),
//     top: "7%",
//     left: "3%",
//   },
//   grid: {
//     top: "20%",
//     left: "3%",
//     right: "4%",
//     bottom: "3%",
//     containLabel: true,
//   },
//   xAxis: {
//     type: "category",
//     boundaryGap: false,
//     data: time,
//   },
//   yAxis: {
//     type: "value",
//     axisLabel: {
//       formatter: "{value} km",
//     },
//     max: 200,
//   },
//   series: [
//     ...data6.map((data) => ({
//       name: data.name,
//       type: "line",
//       data: data.data,
//     })),
//   ],
// });
// const data7 = [
//   {
//     name: "Acceleration",
//     data: tabelData.compredict_vehicle_health_mih_demo.Coaching_acc,
//   },
//   {
//     name: "Braking",
//     data: tabelData.compredict_vehicle_health_mih_demo.Coaching_brake,
//   },
//   {
//     name: "Cornering",
//     data: tabelData.compredict_vehicle_health_mih_demo.Coaching_corn,
//   },
// ];
// const options7 = ref({
//   title: {
//     text: "Coaching",
//     left: "3%",
//   },
//   tooltip: {
//     trigger: "axis",
//     valueFormatter: (value) => value + " %",
//   },
//   legend: {
//     data: data7.map((data) => data.name),
//     top: "7%",
//     left: "3%",
//   },
//   grid: {
//     top: "20%",
//     left: "3%",
//     right: "4%",
//     bottom: "3%",
//     containLabel: true,
//   },
//   xAxis: {
//     type: "category",
//     boundaryGap: false,
//     data: time,
//   },
//   yAxis: {
//     type: "value",
//     axisLabel: {
//       formatter: "{value} %",
//     },
//     max: 100,
//   },
//   series: [
//     ...data7.map((data) => ({
//       name: data.name,
//       type: "line",
//       data: data.data,
//     })),
//   ],
// });
// const data8 = [
//   {
//     name: "SOC",
//     data: carData.compredict_mass_mih_demo.soc,
//   },
// ];
// const options8 = ref({
//   title: {
//     text: "SOC",
//     left: "3%",
//   },
//   tooltip: {
//     trigger: "axis",
//     valueFormatter: (value) => value + " %",
//   },
//   legend: {
//     data: data8.map((data) => data.name),
//     top: "7%",
//     left: "3%",
//   },
//   grid: {
//     top: "20%",
//     left: "3%",
//     right: "4%",
//     bottom: "3%",
//     containLabel: true,
//   },
//   xAxis: {
//     type: "category",
//     boundaryGap: false,
//     data: time,
//   },
//   yAxis: {
//     type: "value",
//     axisLabel: {
//       formatter: "{value} %",
//     },
//     max: 100,
//   },
//   series: [
//     ...data8.map((data) => ({
//       name: data.name,
//       type: "line",
//       data: data.data,
//     })),
//   ],
// });
</script>

<template>
  <div class="text-center selection:bg-green-100">
    <div class="mx-auto grid max-w-[1000px] grid-cols-2 gap-10 px-4">
      <Echarts
        v-for="(data, i) of echartData"
        :key="i"
        :options="data"
      ></Echarts>
      <!-- <Echarts :options="options1"></Echarts>
      <Echarts :options="options2"></Echarts>
      <Echarts :options="options3"></Echarts>
      <Echarts :options="options4"></Echarts>
      <Echarts :options="options5"></Echarts>
      <Echarts :options="options6"></Echarts>
      <Echarts :options="options7"></Echarts>
      <Echarts :options="options8"></Echarts> -->
    </div>
  </div>
</template>

<style></style>
