<template>
    <Product />
    <Buyer />
    <Payment />
</template>

<script>
import Product from './components/Product.vue';
import Buyer from './components/Buyer.vue';
import Payment from './components/Payment.vue';

export default {
  name: 'App',
  components: {
    Product,
    Buyer,
    Payment
  }
}
</script>

<style>
body {
  background: #F6F6F6;
}

#app {
  font-family: Inter, Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  flex-direction: column;
  gap: 24px;
}

.container {
  width: 50vw;
  height: auto;
}

.card {
  width: 100%;
  height: auto;
  border-radius: 4px;
  border: 1px solid #B0B0B0;
  background: white;
}

.content {
  padding: 16px;
}

.input {
  padding: 8px 16px 8px 16px;
  border-radius: 4px;
  border: 1px solid #CED4DA;
  background: #F6F6F6;
  width: 100%;
  box-sizing: border-box;
}
.input-title {
  font-size: 14px;
  font-weight: 400;
  line-height: 21px;
  letter-spacing: 0em;
  text-align: left;
  color: #000000;
  margin-bottom: 2px;
  margin-left: 1px;
}
</style>
