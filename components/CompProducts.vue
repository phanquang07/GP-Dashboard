<template>
  <div class="products">
    <div class="list-products" v-if="listActive === 0">
      <h2>Product 1</h2>
    </div>
    <div class="list-products" v-if="listActive === 1">
      <h2>Product 2</h2>
    </div>
    <div class="list-products" v-if="listActive === 2">
      <h2>Product 3</h2>
    </div>
  </div>
</template>

<script>
export default {
  listActive: 0,
};
</script>

<style>
</style>