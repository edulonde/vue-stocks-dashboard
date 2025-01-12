<template>
  <div class="chart-container">
    <h2>Valor Total por Ação</h2>
    <Bar :data="chartData" :options="chartOptions" />
  </div>
</template>

<script>
import { Bar } from 'vue-chartjs'
import { Chart as ChartJS, CategoryScale, LinearScale, BarElement, Title, Tooltip, Legend } from 'chart.js'

ChartJS.register(CategoryScale, LinearScale, BarElement, Title, Tooltip, Legend)

export default {
  name: 'ValoresChart',
  components: { Bar },
  props: {
    stocks: {
      type: Array,
      required: true
    }
  },
  computed: {
    chartData() {
      return {
        labels: this.stocks.map(stock => stock.codigo),
        datasets: [{
          label: 'Valor Total (R$)',
          data: this.stocks.map(stock => stock.valor),
          backgroundColor: '#42b883'
        }]
      }
    },
    chartOptions() {
      return {
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
          legend: {
            position: 'top',
          }
        }
      }
    }
  }
}
</script>

<style scoped>
.chart-container {
  height: 400px;
  padding: 20px;
  background: white;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
</style>