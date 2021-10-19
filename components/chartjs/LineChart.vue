<template>
  <div class="">
    <line-chart
      :data="LineChartData"
      :options="LineChartOptions"
      :style="styleLineChart"
    />
  </div>
</template>

<script>
import LineChart from "@/components/chartjs/LineChart";

const chartColors = {
  blue: "rgb(72, 128, 255)",
  gray: "rgb(200, 205, 214)",
};

const labels = [
  "",
  "1",
  "2",
  "3",
  "4",
  "5",
  "6",
  "7",
  "8",
  "9",
  "10",
  "11",
  "12",
  "",
];

export default {
  nameLC: 'LineChart',
  components: {
    LineChart,
  },
  data() {
    return {
      LineChartData: {
        labels: labels,
        datasets: [
          {
            label: "Khoảng thời gian này",
            backgroundColor: chartColors.blue,
            data: 
            // this.data_test,
            [, 65, 59, 80, 81, 56, 55, 40, 30, 50, 55, 65, 80],
            fill: false,
            borderColor: chartColors.blue,
            tension: 0.1,
          },
          {
            label: "Khoảng thời gian trước",
            backgroundColor: chartColors.gray,
            data: 
            // this.data_test,
            [, 60, 50, 70, 40, 65, 80, 70, 60, 65, 50, 40, 60],
            fill: false,
            borderColor: chartColors.gray,
            tension: 0.1,
          },
        ],
      },
      LineChartOptions: {
        title: {
          display: true,
          text: ["Khoảng thời gian này", "Khoảng thời gian trước"],
        },
        maintainAspectRatio: false,
        responsive: true,
        legend: {
          display: true,
          position: "bottom",
        },
        title: {
          display: false,
        },
        scales: {
          xAxes: [
            {
              gridLines: {
                drawOnChartArea: false, //cách để xoá đg lưới bên trong
              },
              ticks: {
                display: false,
              },
            },
          ],
          yAxes: [
            {
              display: false,
              ticks: {
                beginAtZero: true, // đặt giới hạn cho trục Y
                steps: 10,
                stepValue: 5,
                max: 100,
              },
            },
          ],
        },
      },
      styleLineChart: {
        width: "100%",
        height: "290px",
      },
    };
  },
};
</script>