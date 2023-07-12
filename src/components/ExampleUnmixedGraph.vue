<template>
  <div class="graph-container">
    <Line :data="data" :options="options" />
  </div>
</template>

<script setup lang="ts">
import {
  Chart as ChartJS,
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  Title,
  Tooltip,
  Legend
} from 'chart.js'

import { Line } from 'vue-chartjs'

ChartJS.register(
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  Title,
  Tooltip,
  Legend
)

const colors = { lightGray: '#ababab' }

const dataPoints = [{ x: 0, y: 0 }, { x: 125, y: 10 }, { x: 250, y: 25 }, { x: 375, y: 10 }]

const data = {
  labels: Array.from(Array(dataPoints.length)),
  datasets: [
    {
      data: dataPoints,
      pointStyle: false,
      borderColor: '#ffd26a'
    }
  ]
}

const fontOptions = (size: number) => ({
  color: colors.lightGray,
  font: {
    family: 'sans-serif',
    size,
    weight: 'bold'
  }
})

const scales = {
  y: {
    title: {
      ...fontOptions(24),
      display: true,
      text: 'Power (dB)'
    },
    grid: { display: false },
    border: { color: 'white', width: 4 },
    ticks: {
      ...fontOptions(40),
      align: 'inner',
      stepSize: 1
    }
    // min: 0,
    // max: 100,
  },
  x: {
    title: {
      ...fontOptions(24),
      display: true,
      text: 'Frequency (Hz)'
    },
    grid: { display: false },
    border: { color: 'white', width: 4 },
    ticks: {
      ...fontOptions(40),
      align: 'inner',
      stepSize: 250,
      beginAtZero: true
    },
    min: 0,
    max: 1000
  },
}

const options = {
  responsive: true,
  maintainAspectRatio: false,
  plugins: {
    legend: { display: false }
  },
  elements: {
    point: { radius: 10 },
    line: { borderWidth: 5 }
  },
  scales
}
</script>

<style>
.graph-container {
  height: 500px;
  width: 500px;
}
</style>
