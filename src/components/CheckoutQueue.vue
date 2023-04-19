<template>
  <div class="checkout-queue">
    <div class="checkout">{{ checkoutNumber }}</div>
    <div class="customer"
    v-for="(purchasesQty, index) in queue"
    :key="index"
    >{{purchasesQty}}</div>
</template>

<script>

export default {

  components: {
  },
  props: {
    queue: {
      type: Array
    },
    checkoutNumber: {
      type: Number
    }
  }
}
</script>
name: 'checkoutQueue'

<style>
 .checkout-queue {
   display: inline-block;
   margin-top: 20px;
   padding: 10px;
 }

 .checkout {
  width: 60px;
  height: 60px;
  border-radius: 10px;
  border: 2px solid gray;
  display: flex;
  align-items: center;
  justify-content: center;
}

.customer {
  width: 60px;
  height: 60px;
  border-radius: 50px;
  border: 2px solid gray;
  margin-top: 15px;
  display: flex;
  align-items: center;
  justify-content: center;

}


</style>
