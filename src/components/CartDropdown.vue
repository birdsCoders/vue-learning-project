<template>
  <div class="dropdown-clip" v-if="cart.length > 0">
    <transition
      name="dropdown"
      @enter="transitionColor"
      @after-leave="resetColor"
    >
      <ul v-if="isOpen" class="list-group">
        <li
          v-for="item in cart"
          :key="item.id"
          class="list-group-item d-flex justify-content-between"
        >
          <span>
            {{ item.name }}
            <span class="badge bg-success align-text-top mr-1">
              {{ item.qty }}
            </span>
          </span>
          <span><currency :amount="item.price" /></span>
          <button
            @click.stop="this.$parent.$emit('deleteItem', item.id)"
            class="btn btn-sm btn-danger ml-2"
          >
            -
          </button>
        </li>
      </ul>
    </transition>
    <router-link
      to="/checkout"
      class="btn btn-sm btn-success text-white float-right mr-2 mt-2"
    >
      checkout</router-link
    >
  </div>
</template>

<script>
import Currency from './Currency';
export default {
  data: function () {
    return {
      totalColor: 'text-secondary',
    };
  },
  props: ['cart', 'isOpen'],
  components: {
    Currency,
  },
  methods: {
    transitionColor(el) {
      this.totalColor = 'text-danger';
    },
    resetColor() {
      this.totalColor = 'text-secondary';
    },
  },
};
</script>

<style>
.dropdown-clip {
  overflow: hidden;
}

.dropdown-enter-active,
.dropdown-leave-active {
  transition-property: transform, opacity;
  transition-duration: 0.5s;
  transition-timing-function: ease-in-out;
  transform: auto;
}

.dropdown-enter-from,
.dropdown-leave-to {
  transform: translateY(-300px);
  opacity: 0;
}
</style>
