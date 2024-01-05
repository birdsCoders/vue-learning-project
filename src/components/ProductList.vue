<template>
  <transition-group appear name="products">
    <div
      class="row align-items-center"
      v-for="product in products"
      :key="product.id"
    >
      <product :product="product" :key="product.id"></product>
    </div>
  </transition-group>
</template>

<script>
import Product from '@/components/Product';
export default {
  props: ['products'],
  components: {
    Product,
  },
};
</script>

<style>
.products-enter-active,
.products-leave-active {
  transition-property: transform, opacity;
  transition-duration: 0.5s;
  transition-timing-function: ease-in-out;
}

.products-enter-from {
  transform: translateX(300px);
  opacity: 0;
}

.products-leave-to {
  transform: translateX(-300px);
  opacity: 0;
}
</style>
