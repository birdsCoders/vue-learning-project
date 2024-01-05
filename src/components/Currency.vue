<template>
  {{ calc(amount) }}
</template>

<script>
export default {
  props: ['amount'],
  methods: {
    calc(value) {
      return `$${Number.parseFloat(value).toFixed(2)}`;
    },
  },
};
</script>
