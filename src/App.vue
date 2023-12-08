<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import { ref, computed } from "vue";
import dayjs from "dayjs";
import Echarts from "./components/Echarts.vue";
import carData from "./assets/mock/carJson.json";
// import tabelData from "./assets/mock/tabelJson.json";
// import axios from "axios";

// async function getData() {
//   const { data } = await axios.get(
//     "https://app-mih-fms-dev-001.azurewebsites.net/v1/ivy_insights/mass"
//   );
//   console.log(data);
// }
// getData();
const time = carData.Timestamp.map((time) => dayjs(time).format("HH:mm"));
let now = new Date();
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
let dynamicData = [];
for (let i = 0; i < 5; i++) {
  dynamicData.push(randomData());
}
const fetchData = ref([
  {
    title: "SOC",
    unit: "%",
    xAxis: {
      data: [
        "2023-12-03T14:23:41.756952Z",
        "2023-12-04T14:23:41.756952Z",
        "2023-12-05T14:23:41.756952Z",
        "2023-12-06T14:23:41.756952Z",
        "2023-12-07T14:23:41.756952Z",
      ],
    },
    yAxis: {
      max: 100,
    },
    data: [
      {
        name: "SOC",
        data: [73, 70, 68, 66, 63],
      },
    ],
  },
]);
setInterval(() => {
  now = new Date(+now + oneDay);
  fetchData.value[0].xAxis.data.push(now.toString());
  fetchData.value[0].data[0].data.push(Math.round(value));
  console.log("111");
}, 5000);
const dynamicMapData = computed(() => {
  const dynamicMapData = fetchData.value.map((data, i) => {
    return {
      title: data.title,
      unit: data.unit,
      data: data.xAxis.data.map((_, index) => {
        return {
          name: data.xAxis.data[index],
          value: [
            dayjs(data.xAxis.data[index]).format("YYYY/MM/DD"),
            data.data[0].data[index],
          ],
        };
      }),
      dynamic: true,
    };
  });
  return dynamicMapData;
});
console.log(dynamicMapData.value);
// {
//   index: 4,
//   title: "Effect remaining range",
//   unit: "km",
//   data: dynamicData,
//   dynamic: true,
// },
console.log(dynamicData);
const echartData = computed(() =>
  [
    // {
    //   index: 1,
    //   title: "Pad wear",
    //   unit: "%",
    //   xAxis: {
    //     data: ["current", "1000", "1500", "2000", "2500"],
    //   },
    //   yAxis: {
    //     max: 100,
    //   },
    //   data: [
    //     {
    //       name: "front pad wear",
    //       data: [53.4, 52.1, 50.8, 50.3, 50],
    //     },
    //     {
    //       name: "rear pad wear",
    //       data: [47.4, 46, 44.7, 43.5, 42.1],
    //     },
    //   ],
    // },
    // {
    //   index: 2,
    //   title: "Vehicle mess",
    //   unit: "kg",
    //   xAxis: {
    //     data: time,
    //   },
    //   data: [
    //     {
    //       name: "Truck weight",
    //       data: Array(3).fill(2500),
    //     },
    //     {
    //       name: "Payload",
    //       data: [1000, 1100, 1200],
    //     },
    //   ],
    //   stack: true,
    // },
    // {
    //   index: 3,
    //   title: "Tire wear",
    //   unit: "%",
    //   xAxis: {
    //     data: ["current", "1000", "1500", "2000", "2500"],
    //   },
    //   yAxis: {
    //     max: 100,
    //   },
    //   data: [
    //     {
    //       name: "front left tire wear",
    //       data: [34.1, 27.6, 24.1, 20.8, 17.5],
    //     },
    //     {
    //       name: "front right tire wear",
    //       data: [34.5, 29.8, 26.8, 23.5, 20.3],
    //     },
    //     {
    //       name: "Rear left tire wear",
    //       data: [20.3, 13.5, 9.9, 6.3, 3.5],
    //     },
    //     {
    //       name: "Rear right tire wear",
    //       data: [21.7, 15.9, 12.6, 8.9, 5.5],
    //     },
    //   ],
    // },
    ...dynamicMapData.value,
    {
      index: 4,
      title: "Effect remaining range",
      unit: "km",
      data: dynamicData,
      dynamic: true,
    },
    // {
    //   index: 5,
    //   title: "Battery",
    //   unit: "%",
    //   xAxis: {
    //     data: ["current", "1000", "1500", "2000", "2500"],
    //   },
    //   yAxis: {
    //     max: 100,
    //   },
    //   data: [
    //     {
    //       name: "Battery",
    //       data: [76.8, 76.6, 76.2, 75.7, 75.1],
    //     },
    //   ],
    // },
    // {
    //   index: 6,
    //   title: "Speed",
    //   unit: "km",
    //   xAxis: {
    //     data: time,
    //   },
    //   yAxis: {
    //     max: 200,
    //   },
    //   data: [
    //     {
    //       name: "Speed",
    //       data: [20, 50, 70],
    //     },
    //   ],
    // },
    // {
    //   index: 8,
    //   title: "Coaching",
    //   unit: "%",
    //   xAxis: {
    //     data: time,
    //   },
    //   yAxis: {
    //     max: 100,
    //   },
    //   data: [
    //     {
    //       name: "Acceleration",
    //       data: [92, 91, 90],
    //     },
    //     {
    //       name: "Braking",
    //       data: [98, 97, 96],
    //     },
    //     {
    //       name: "Cornering",
    //       data: [91, 90, 89],
    //     },
    //   ],
    // },
    // {
    //   index: 7,
    //   title: "SOC",
    //   unit: "%",
    //   xAxis: {
    //     data: time,
    //   },
    //   yAxis: {
    //     max: 100,
    //   },
    //   data: [
    //     {
    //       name: "SOC",
    //       data: [73, 72, 71],
    //     },
    //   ],
    // },
  ].sort((a, b) => a.index - b.index)
);
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
