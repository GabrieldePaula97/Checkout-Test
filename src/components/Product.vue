<template>
  <div class="container">
    <div class="card">
      <div class="content product-container">
        <div class="product-image">
          <img src="@/assets/product.png" alt="product image">
        </div>
        <div class="product-data">
          <span class="product-name"> Nome do Produto </span>
          <span class="product-price"> R$ 500,00 / mês </span>
          <span class="product-info"> Plano mensal com renovação automática </span>
        </div>
      </div>
      <div class="footer">
        <span class="contact">contatolivrediet@gmail.com</span>
      </div>
    </div>
  </div>
  
</template>

<script>
export default {
  name: 'ProductData',
  props: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.product-container{
  display: grid;
  grid-template-columns: 2fr 6fr;
  max-width: 100%;
  width: var(--max-width);
}

.product-data {
  display: flex;
  align-items: flex-start;
  justify-content: center;
  flex-direction: column;
  row-gap: 8px;
}

.product-image {
  display: flex;
  border-radius: 4px;
}

.product-name {
  font-size: 16px;
  font-weight: 700;
  line-height: 19px;
  letter-spacing: 0em;
  text-align: left;
}

.product-price {
  font-size: 20px;
  font-weight: 600;
  line-height: 24px;
  letter-spacing: 0em;
  text-align: left;
  color: #FF6905;
}

.product-info {
  font-size: 12px;
  font-weight: 400;
  line-height: 15px;
  letter-spacing: 0em;
  text-align: left;
  color: #303133;
}

.footer {
  display: flex;
  max-height: 36px;
  padding: 8px 16px 8px 16px;
  border-radius: 0px 0px 4px 4px;
  border: 0px 1px 1px 1px;
  background: #FF6905;
}

.contact {
  font-size: 12px;
  font-weight: 600;
  line-height: 19px;
  letter-spacing: 0em;
  text-align: left;
  color: #FBFBFB;
}
</style>
