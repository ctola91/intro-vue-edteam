<template>
  <h1>Product {{ productId }}</h1>
</template>
<script>
import { useRoute } from "vue-router";
export default {
  setup() {
    const route = useRoute();
    const productId = route.params.productId;

    return {
      productId,
    };
  },
};
</script>