<template>
  <div class="checkout">{{ checkoutNumber }}</div>
</template>

<script>
export default {
  props: {
    queues: {
      type: Array,
    },
    checkoutNumber: {
      type: Number,
    },
  },
};
</script>
name: 'checkout'

<style>
.checkout {
  width: 60px;
  height: 60px;
  border-radius: 10px;
  border: 2px solid gray;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
