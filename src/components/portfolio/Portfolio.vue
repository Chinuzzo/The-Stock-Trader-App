<template>
  <div>
    <app-stock
      v-for="(stock, key) in stocks"
      :key="key"
      :stock="stock"
    ></app-stock>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';
import Stock from './Stock.vue';

export default {
  components: {
    appStock: Stock,
  },
  computed: {
    ...mapGetters({
      stocks: 'stockPortfolio',
    }),
  },
};
</script>
