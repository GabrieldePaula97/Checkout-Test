<template>
  <div class="container">
    <div class="card">
      <div class="content">
        <div class="name-container">
          <span class="input-title"> Nome Completo </span>
          <input class="input" type="text" name="Nome Completo" id="name" placeholder="Digite seu nome completo">
        </div>
        <div class="contact-container">
          <div class="contact-input-container">
            <span class="input-title"> E-mail </span>
            <input class="input" type="text" name="E-mail" id="e-mail" placeholder="Digite seu e-mail">
          </div>
          <div class="contact-input-container">
            <span class="input-title"> Telefone </span>
            <input class="input" type="text" name="Telefone" id="tel" placeholder="(00) x0000-0000">
          </div>
        </div>
      </div>
    </div>
  </div>
  
</template>

<script>
export default {
  name: 'BuyerData',
  props: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card {
  background: #F6F6F6!important;
}
.name-container, .contact-input-container {
  display: flex;
  align-items: flex-start;
  justify-content: center;
  flex-direction: column;
  width: 100%;
}

.name-container {
  margin-bottom: 10px;
}

.contact-container {
  display: grid;
  grid-template-columns: 6fr 4fr;
  max-width: 100%;
  width: var(--max-width);
  column-gap: 32px;
}

</style>
