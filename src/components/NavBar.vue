<template>
  <nav class="navbar navbar-light">
    <div
      v-if="cart.length"
      class="w-100 navbar-text ml-auto d-flex justify-content-end position-relative"
    >
      <div
        class="mr-auto d-flex align-items-end flex-column bd-highlight mb-3 position-absolute"
      >
        <div class="mb-2">
          <span class="font-weight-bold bg-white"
            ><currency :amount="cartTotal"></currency
          ></span>
          <button
            :class="cartBtn"
            @click="toggleCartMenu"
            class="btn btn-sm ms-2"
            aria-haspopup="true"
            aria-expanded="false"
          >
            <fa icon="shopping-cart" />
            <span class="ms-2">{{ cartQty }}</span>
          </button>
        </div>
        <cart-dropdown :is-open="displayCart" :cart="cart" />
      </div>
    </div>
  </nav>
</template>

<script>
import Currency from './Currency';
import CartDropdown from './CartDropdown';

export default {
  data: function () {
    return {
      displayCart: false,
    };
  },
  props: ['cart', 'cartTotal', 'cartQty'],
  components: {
    Currency,
    CartDropdown,
  },
  computed: {
    cartBtn() {
      return {
        'btn-secondary': this.cartTotal <= 100,
        'btn-success': this.cartTotal > 100,
        'btn-danger': this.cartTotal > 200,
      };
    },
  },
  methods: {
    toggleCartMenu() {
      this.displayCart = !this.displayCart;
    },
  },
};
</script>
