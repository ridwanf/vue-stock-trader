<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light mb-3">
    <router-link to='/' class="navbar-brand">Stock Trader</router-link>
    <div class="collapse navbar-collapse">
      <ul class="navbar-nav mr-auto">
        <router-link to="/portfolio" active-class="active nav-item" tag="li">
          <a class="nav-link">Portfolio</a>
        </router-link>
        <router-link to="/stocks" active-class="active nav-item" tag="li">
          <a class="nav-link">Stocks</a>
        </router-link>
      </ul>
      <ul class="navbar-nav pull-xs-right ">
        <li active-class="nav-item active">
          <a class="nav-link" href="#" @click="endDay">End Day</a>
        </li>
        <li active-class="nav-item active">
          <a class="dropdown-item" href="#" @click="saveData">Save Data</a>
        </li>
        <li active-class="nav-item active">
          <a class="dropdown-item" href="#" @click="loadData">Load Data</a>
        </li>
      </ul>
      <strong class="navbar-item pull-xs-right">Funds: {{funds | currency}}</strong>
    </div>
  </nav>
</template>

<script>
import { mapActions } from 'vuex';

export default {
  data() {
    return {
      isDropdownOpen: false
    }
  },
  computed: {
    funds() {
      return this.$store.getters.funds;
    }
  },
  methods: {
    ...mapActions({
      randomizeStocks: 'randomizeStocks',
      fetchData: 'loadData'
    }),
    endDay() {
      this.randomizeStocks();
    },
    saveData() {
      const data = {
        funds: this.$store.getters.funds,
        stockPortfolio: this.$store.getters.stockPortfolio,
        stocks: this.$store.getters.stocks
      };
      this.$http.put('data.json', data);
    },
    loadData() {
      this.fetchData();
    }
  }
}
</script>