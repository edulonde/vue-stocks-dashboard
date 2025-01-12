<template>
  <div class="" id="app">
    <h1 class="text-4xl text-red-600">Dashboard de Ações</h1>

    <!-- Tabela de Ações -->
    <StocksTable :stocks="stocks" />

    <!-- Gráficos -->
    <div class="charts">
      <ValoresChart :stocks="stocks" />
      <QuantidadeChart :stocks="stocks" />
    </div>
  </div>
</template>

<script>
import StocksTable from './components/StocksTable.vue'
import ValoresChart from './components/ValoresChart.vue'
import QuantidadeChart from './components/QuantidadeChart.vue'
import stocksData from './data/stocks.json'

export default {
  name: 'App',
  components: {
    StocksTable,
    ValoresChart,
    QuantidadeChart
  },
  data() {
    return {
      stocks: stocksData.stocks
    }
  }
}
</script>

<style>
#app {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.charts {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
  margin-top: 20px;
}

@media (max-width: 768px) {
  .charts {
    grid-template-columns: 1fr;
  }
}
</style>