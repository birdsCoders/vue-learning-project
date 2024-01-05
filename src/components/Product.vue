<template>
  <div class="col card">
    <div class="col-sm-2 m-auto">
      <button
        class="btn btn-success mt-3"
        @click="this.$parent.$parent.$parent.$emit('addItem', product)"
      >
        + Add
      </button>
    </div>
    <div class="col-sm-4">
      <img class="img-thumbnail" :src="product.image" :alt="product.name" />
    </div>
    <div class="col-sm-6">
      <h3 class="text-primary">{{ index + 1 }} {{ product.name }}</h3>
      <p class="mb-0">{{ product.description }}</p>
      <div class="h5 float-right">
        <div class="tag tag-high" v-if="product.price >= Number(max)">
          premier
        </div>
        <div
          class="tag tag-low"
          v-else-if="product.price < Number(max) && product.price > Number(min)"
        >
          value
        </div>
        <div class="tag tag-sale" v-else-if="product.price < Number(min)">
          sale
        </div>
        <currency :amount="product.price"></currency>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      max: 100,
      min: 85,
    };
  },
  props: ['product'],
  emits: ['addItem'],
};
</script>

<style scoped lang="scss">
.img-thumbnail {
  max-width: 200px;
}

.card {
  padding: 20px;
  margin-bottom: 30px;
  flex-direction: row;
}

.tag {
  background: gray;
  padding: 5px;
  color: white;
  width: 100px;

  &-high {
    background: green;
  }

  &-low {
    background: blue;
  }

  &-sale {
    background: red;
  }
}
</style>
