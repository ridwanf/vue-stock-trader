<template>
  <div class="col-sm-3 col-md-4">
    <div class="card text-white  mb-3">
      <div class="card-header bg-info">{{stock.name}}
        <small>(Price: {{stock.price}} | Quantity: {{stock.quantity}})</small>
      </div>
      <div class="card-body">
        <div class="form-inline">
          <input :class="{'is-invalid': insufficientQuantity}" type="number" class="form-control mr-3" placeholder="Quantity" v-model="quantity">
          <button class="btn-success btn" @click="sellStock" :disabled="insufficientQuantity|| quantity<=0 || Number.isInteger(quantity)">
            {{insufficientQuantity ? 'Not enough Stocks':'sell'}}
          </button>
        </div>

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
      quantity: 0
    }
  },
  computed: {
    insufficientQuantity() {
      return this.quantity > this.stock.quantity;
    }
  },
  methods: {
    ...mapActions({
      placeSellOrder: 'sellStock'
    }),
    sellStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      };
      // this.$store.dispatch('buyStock', order);
      this.placeSellOrder(order);
      this.quantity = 0;
    }
  }
}
</script>