<template>
  <h1></h1>
<!--   <v-chart class="chart" :option="option" autoresize />
  <h1></h1>
    <v-chart class="chart" :option="option2" autoresize />
  <h1></h1> -->
    <v-chart class="chart" :option="option3" autoresize ref="chartRef" />

</template>

<script setup>
import { use } from 'echarts/core';
import { CanvasRenderer } from 'echarts/renderers';
import { LineChart, PieChart } from 'echarts/charts';
import {
  TitleComponent,
  TooltipComponent,
  LegendComponent,
} from 'echarts/components';
import VChart, { THEME_KEY} from 'vue-echarts';
import { ref, provide, onMounted } from 'vue';
import { GridComponent } from 'echarts/components';

use([
  GridComponent,
  CanvasRenderer,
  LineChart,
  PieChart,
  TitleComponent,
  TooltipComponent,
  LegendComponent,
]);

provide(THEME_KEY, 'light');

// line chart
const option = ref({
  xAxis: {
    type: 'category',
    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
  },
  yAxis: {
    type: 'value'
  },
  series: [
    {
      data: [150, 230, 224, 218, 135, 147, 260],
      type: 'line'
    }
  ]
});



var colorPalette = ['#2563eb','#10b981', '#ffbf00', '#ff0000', '#a78bfa']
// pie chart
const option2 = ref({
  title: {
    text: 'Traffic Sources',
    left: 'center',
  },
  tooltip: {
    trigger: 'item',
    formatter: '{a} <br/>{b} : {c} ({d}%)',
  },
  legend: {
    orient: 'vertical',
    left: 'left',
    data: ['Direct', 'Email', 'Ad Networks', 'Video Ads', 'Search Engines'],
  },
  series: [
    {
      name: 'Traffic Sources',
      type: 'pie',
      radius: '55%',
      center: ['50%', '60%'],
      data: [
        { value: 335, name: 'Direct' },
        { value: 310, name: 'Email' },
        { value: 234, name: 'Ad Networks' },
        { value: 135, name: 'Video Ads' },
        { value: 1548, name: 'Search Engines' },
      ],
      color: colorPalette,
      // emphasis: {
      //   itemStyle: {
      //     shadowBlur: 10,
      //     shadowOffsetX: 0,
      //     shadowColor: 'red',
      //   },
      // },
    },
  ],
});

const colorPalettez = ['#93c5fd', '#7dd3fc', '#1e3a8a', '#172554'];
const option3 = ref({
  backgroundColor: '',
  title: {
    text: 'Customized Pie',
    left: 'center',
    top: 20,
    textStyle: {
      color: '#000'
    }
  },
  tooltip: {
    trigger: 'item'
  },

  series: [
    {
      name: 'Access From',
      type: 'pie',
      radius: ['40%', '70%'],
      // center: ['50%', '50%'],
      data: [
        { value: 50, name: 'Direct' },
        { value: 310, name: 'Email' },
        { value: 274, name: 'Union Ads' },
        { value: 235, name: 'Video Ads' },
      ].sort(function (a, b) {
        return a.value - b.value;
      }),
      // roseType: 'radius',
  label: {
     // formatter : "{b}\n{d}%",

    formatter: '{d}%', // Percentage text
    position: 'inside', // Keep labels inside the pie slices
    color: "#333",
    fontSize: 20,
    backgroundColor: "#fff", // White background for labels
    borderRadius: 9999, // Circular labels
    height: 120,
    width: 120,
    borderWidth: 1,
    borderColor: '#333',
    distance: 0,
    overflow: 'truncate', // Ensure text stays within boundaries


        // height: '50px'
        //  formatter: () => {
        //   return sum; // Use sum variable here
        // },
      },
      percentPrecision: 0,
      emphasis: {
        label: { show: true },
        itemStyle: {
          shadowBlur: 10,
          shadowOffsetX: 0,
          shadowColor: 'rgba(0, 0, 0, 0.5)'
        }
      },
      labelLine: {
        lineStyle: {
          color: '#333'
        },
        smooth: 0.2,
        length: 60,
        length2: 20
      },
    color: colorPalettez,
      itemStyle: {
        // shadowBlur: 200,
        // shadowColor: 'rgba(0, 0, 0, 0.5)'
      },
      animationType: 'scale',
      animationEasing: 'elasticOut',
      animationDelay: function (idx) {
        return Math.random() * 200;
      }
    }
  ]
});

const chartRef = ref(null);
let currentIndex = -1;

// onMounted(() => {
//   const interval = setInterval(() => {
//     // Ensure the chart instance exists
//     console.log("chartref", chartRef);
//     if (chartRef.value) {
//       const dataLen = 4; // Get data length

//       // Downplay the current highlighted data point
//       if (currentIndex >= 0) {
//         chartRef.value.dispatchAction({
//           type: 'downplay',
//           seriesIndex: 0,
//           dataIndex: currentIndex,
//         });
//       }

//       // Update the currentIndex and loop back if it exceeds data length
//       currentIndex = (currentIndex + 1) % dataLen;

//       // Highlight the next data point
//       chartRef.value.dispatchAction({
//         type: 'highlight',
//         seriesIndex: 0,
//         dataIndex: currentIndex,
//       });

//       // Show the tooltip for the highlighted data point
//       chartRef.value.dispatchAction({
//         type: 'showTip',
//         seriesIndex: 0,
//         dataIndex: currentIndex,
//       });
//     } else {
//       console.warn("Chart instance not initialized yet.");
//     }
//   }, 1000);

//   // Cleanup the interval when the component is unmounted
// });
</script>



<style scoped>
  h1 {
    text-align: center;
    margin-bottom: 100px;
  }

.chart {
  height: 700px;
}
</style>
