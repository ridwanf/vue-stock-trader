<template>
  <div class="col-sm-3 col-md-4">
    <div class="card text-white  mb-3">
      <div class="card-header bg-success">{{stock.name}}
        <small>(Price: {{stock.price}})</small>
      </div>
      <div class="card-body">
        <div class="form-inline">
          <input :class="{'is-invalid': insufficientFunds}" type="number" class="form-control mr-3" placeholder="Quantity" v-model="quantity">
          <button class="btn-success btn" @click="buyStock" :disabled="insufficientFunds||quantity<=0 || Number.isInteger(quantity)">
            {{insufficientFunds?'Insufficient Funds ':'Buy '}}
          </button>
        </div>

      </div>
    </div>
  </div>
</template>
<style scoped>

</style>

<script>
export default {
  props: ['stock'],
  data() {
    return {
      quantity: 0
    }
  },
  computed: {
    funds() {
      return this.$store.getters.funds;
    },
    insufficientFunds() {
      return this.quantity * this.stock.price > this.funds;
    }
  },
  methods: {
    buyStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      };
      this.$store.dispatch('buyStock', order);
      this.quantity = 0
    }
  }
}
</script>