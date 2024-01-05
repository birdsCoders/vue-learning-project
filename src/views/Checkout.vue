<template>
  <div class="container">
    <h1>Checkout</h1>

    <table class="table table-hover" v-if="cart.length">
      <caption class="text-right h3">
        <b>Total:</b>
        <currency :amount="cartTotal"></currency>
      </caption>
      <thead>
        <tr>
          <th scope="col"></th>
          <th scope="col">Item</th>
          <th scope="col" class="text-center">Qty</th>
          <th scope="col" class="text-right">Price</th>
          <th scope="col" class="text-right">Sub-total</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(product, index) in cart" :key="index">
          <td class="text-center">
            <div class="btn-group" role="group" aria-label="Basic example">
              <button
                @click="this.$emit('addItem', product)"
                class="btn btn-success"
              >
                +
              </button>
              <button
                @click="this.$emit('deleteItem', product.id)"
                class="btn btn-outline-success"
              >
                -
              </button>
            </div>
          </td>
          <th scope="row">{{ product.name }}</th>
          <td class="text-center">{{ product.qty }}</td>
          <td class="text-right">
            <currency :amount="Number(product.price)"></currency>
          </td>
          <td class="text-right">
            <currency :amount="product.qty * Number(product.price)"></currency>
          </td>
        </tr>
      </tbody>
    </table>
    <router-link class="btn btn-sm btn-success" to="/"
      >Keep Shopping</router-link
    >
  </div>
</template>

<script>
import Currency from '@/components/Currency';
export default {
  props: ['cart', 'cartTotal'],
  components: {
    Currency,
  },
  emits: ['addItem', 'deleteItem'],
};
</script>

<style></style>
