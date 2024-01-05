<template>
  <div class="mb-3">
    <div class="mb-2">
      <label for="max-price" class="form-label"
        >Max price: ${{ modelValue }}</label
      >
      <input
        type="range"
        class="form-range"
        min="0"
        max="130"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
      />
    </div>
    <div class="badge bg-success">
      <b>Search results:</b> {{ products.length }}
    </div>
  </div>
</template>

<script>
export default {
  props: ['modelValue', 'products'],
};
</script>
