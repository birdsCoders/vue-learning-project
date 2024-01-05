<template>
  <div
    class="alert"
    :class="[
      type ? 'alert-' + type : 'alert-secondary',
      close ? 'alert-dismissible' : '',
    ]"
  >
    <slot>Congradulations on getting some items into the cart</slot>
    <button
      class="btn-close"
      type="button"
      aria-label="close"
      v-if="close"
      @click="closeButton"
    ></button>
  </div>
</template>

<script>
export default {
  props: ['close', 'type'],
  methods: {
    closeButton() {
      event.target.parentNode.remove();
    },
  },
};
</script>
