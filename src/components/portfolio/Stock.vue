<template>
  <div class="col-sm-6 col-md-4">
    <div class="card">
      <h3 class="card-title-info">
        {{ stock.name }}
        <small
          >(Price: {{ stock.price }} | Quantity: {{ stock.quantity }})</small
        >
      </h3>
    </div>
    <div class="card-body">
      <div class="pull-left">
        <input
          type="number"
          class="form-control"
          placeholder="Quantity"
          v-model.number="quantity"
          :class="{ danger: insufficientQuantity }"
        />
      </div>
      <div class="pull-right">
        <button
          class="btn btn-success"
          @click="sellStock"
          :disabled="
            insufficientQuantity || quantity <= 0 || !Number.isInteger(quantity)
          "
        >
          {{ insufficientQuantity ? 'Not enough' : 'Sell' }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex';

export default {
  props: ['stock'],
  data() {
    return {
      quantity: 0,
    };
  },
  computed: {
    insufficientQuantity() {
      return this.quantity > this.stock.quantity;
    },
  },
  methods: {
    ...mapActions({
      placeSellOrder: 'sellStock',
    }),
    sellStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity,
      };
      this.placeSellOrder(order);
      console.log(order);
      this.quantity = 0;
    },
  },
};
</script>

<style scoped>
.danger {
  border: 2px solid red;
}

.card-title-info {
  background-color: lightcoral;
  padding: 8px;
  border-radius: 0.375rem;
}
</style>
