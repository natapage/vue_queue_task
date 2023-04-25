<template>
  <div id="app">
    <h2 style="color: red" v-if="!isCorrectQuantity">
      please enter a positive integer
    </h2>
    <div class="input-form">
      <input
        v-model="newPurchasesQuantity"
        type="number"
        class="input"
        placeholder="Add purchases quantity.."
      />
      <button class="btn" @click="addCustomer">Create customer!</button>
    </div>

    <div class="checkout-zone">
      <checkoutQueue
        v-for="(checkoutQueue, index) in queues"
        :key="index + 1"
        :checkoutNumber="index + 1"
        :queue="queues[index]"
      />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'Vue';
import checkoutQueue from './components/CheckoutQueue.vue';

const queues = ref([[2, 3, 5], [2, 6, 3], [1], [11, 3, 6], []]);
const newPurchasesQuantity = ref('');
const isCorrectQuantity = ref(true);

function addCustomer() {
  newPurchasesQuantity = Number(newPurchasesQuantity);
  if (newPurchasesQuantity > 0 && Number.isInteger(newPurchasesQuantity)) {
    isCorrectQuantity = true;
    queues[shortestQueueIndex].push(newPurchasesQuantity);
    newPurchasesQuantity = '';
    return;
  }
  isCorrectQuantity = false;
  newPurchasesQuantity = '';
}

function updateQueues() {
  queues.forEach((queue) => {
    if (queue.length === 0) {
      return;
    }
    if (queue[0] === 1) {
      queue.shift();
      return;
    }
    queue[0] -= 1;
  });
}

onMounted(() => setInterval(updateQueues, 2000));

const shortestQueueIndex = computed(() => {
  return queues
    .map((array, index) => {
      return array.reduce((acc, item) => acc + item, 0);
    })
    .reduce((acc, item, index, arr) => (item < arr[acc] ? index : acc), 0);
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.checkout-zone {
  display: flex;
}
</style>
