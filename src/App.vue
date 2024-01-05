<template>
  <navbar
    :cart="cart"
    :cart-total="cartTotal"
    :cart-qty="cartQty"
    @delete-item="deleteItem"
  />
  <div class="container">
    <router-view
      :products="products"
      :cart="cart"
      @add-item="addItem"
      @delete-item="deleteItem"
      :cart-total="cartTotal"
    />
  </div>
</template>

<script>
import Navbar from '@/components/NavBar';
export default {
  data: function () {
    return {
      cart: [],
      products: [],
    };
  },
  components: {
    Navbar,
  },
  created() {
    fetch('https://hplussport.com/api/products/order/price')
      .then((response) => response.json())
      .then((data) => (this.products = data))
      .catch((err) => console.log(err));
  },
  computed: {
    cartTotal() {
      return this.cart.reduce(
        (acc, item) => acc + Number(item.price) * Number(item.qty),
        0,
      );
    },
    cartQty() {
      return this.cart.reduce((acc, item) => acc + Number(item.qty), 0);
    },
  },
  methods: {
    addItem(product) {
      const current = this.cart.find((item) => item.id === product.id);

      if (current) {
        current.qty++;
      } else {
        this.cart.push({ ...product, qty: 1 });
      }
    },
    deleteItem(id) {
      const current = this.cart.find((item) => item.id === id);

      if (current.qty > 1) {
        current.qty--;
      } else {
        this.cart = this.cart.filter((item) => item.id !== id);
      }
    },
  },
};
</script>

<style lang="scss">
$primary: #6f42c1;
@import 'node_modules/bootstrap/scss/bootstrap';
</style>
