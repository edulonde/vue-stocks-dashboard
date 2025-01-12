<template>
  <div class="stocks-table">
    <table>
      <thead>
      <tr>
        <th @click="sort('codigo')">Código</th>
        <th @click="sort('nome')">Nome</th>
        <th @click="sort('preco')">Preço</th>
        <th @click="sort('quantidade')">Quantidade</th>
        <th @click="sort('valor')">Valor</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="stock in sortedStocks" :key="stock.codigo">
        <td>{{ stock.codigo }}</td>
        <td>{{ stock.nome }}</td>
        <td>R$ {{ stock.preco.toFixed(2) }}</td>
        <td>{{ stock.quantidade }}</td>
        <td>R$ {{ stock.valor.toFixed(2) }}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'StocksTable',
  props: {
    stocks: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      sortKey: 'codigo',
      sortOrders: {
        codigo: 1,
        nome: 1,
        preco: 1,
        quantidade: 1,
        valor: 1
      }
    }
  },
  computed: {
    sortedStocks() {
      return [...this.stocks].sort((a, b) => {
        const order = this.sortOrders[this.sortKey]
        return (a[this.sortKey] > b[this.sortKey] ? 1 : -1) * order
      })
    }
  },
  methods: {
    sort(key) {
      if (key === this.sortKey) {
        this.sortOrders[key] = this.sortOrders[key] * -1
      }
      this.sortKey = key
    }
  }
}
</script>

<style scoped>
.stocks-table {
  margin: 20px 0;
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  padding: 12px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

th {
  cursor: pointer;
  background-color: #f5f5f5;
}

th:hover {
  background-color: #e5e5e5;
}

tr:hover {
  background-color: #f9f9f9;
}
</style>