<template>
  <range-selector v-model="maxPrice" :products="filteredProducts" />
  <product-list :products="filteredProducts" />
</template>

<script>
import ProductList from '@/components/ProductList';
import RangeSelector from '@/components/RangeSelector';

export default {
  name: 'HomeView',
  data() {
    return {
      maxPrice: 100,
    };
  },
  props: ['products'],
  components: {
    ProductList,
    RangeSelector,
  },
  computed: {
    filteredProducts() {
      return this.products.filter((item) => item.price < Number(this.maxPrice));
    },
  },
  methods: {
    addToCart(product) {
      this.cart.push(product);
    },
  },
};
</script>
