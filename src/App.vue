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

<script>
import checkoutQueue from './components/CheckoutQueue.vue';

export default {
  data() {
    return {
      queues: [[2, 3, 5], [2, 6, 3], [1], [11, 3, 6], []],
      newPurchasesQuantity: '',
      isCorrectQuantity: true
    };
  },
  name: 'App',
  components: {
    checkoutQueue,
  },
  methods: {
    addCustomer() {
      this.newPurchasesQuantity = Number(this.newPurchasesQuantity);
      if (
        this.newPurchasesQuantity > 0 &&
        Number.isInteger(this.newPurchasesQuantity)
      ) {
        this.isCorrectQuantity = true;
        this.queues[this.shortestQueueIndex].push(
          this.newPurchasesQuantity);
        this.newPurchasesQuantity = '';
        return
        }
      this.isCorrectQuantity = false;
      this.newPurchasesQuantity = '';
    },
    updateQueues() {
      this.queues.forEach((queue) => {
        if (queue.length === 0) {
          return;
        }
        if (queue[0] === 1) {
          queue.shift();
          return;
        }
        queue[0] -= 1;
      });
    },
  },
  mounted() {
    setInterval(this.updateQueues, 2000);
  },
  computed: {
    shortestQueueIndex() {
      return this.queues
        .map((array, index) => {
          return array.reduce((acc, item) => acc + item, 0);
        })
        .reduce((acc, item, index, arr) => (item < arr[acc] ? index : acc), 0);
    },
  },
};
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
