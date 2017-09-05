<template>
  <div class="col-sm-3 col-md-4">
    <div class="card text-white  mb-3">
      <div class="card-header bg-info">{{stock.name}}
        <small>(Price: {{stock.price}})</small>git
      </div>
      <div class="card-body">
        <div class="form-inline">
          <input type="number" class="form-control mr-3" placeholder="Quantity" v-model="quantity">
          <button class="btn-success btn" @click="buyStock" :disabled="quantity<=0 || !Number.isInteger(quantity)">
            Buy
          </button>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['stock'],
  data() {
    return {
      quantity: 0
    }
  },
  methods: {
    buyStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      };
      this.quantity = 0
    }
  }
}
</script>