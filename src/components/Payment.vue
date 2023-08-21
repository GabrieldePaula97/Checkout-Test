<template>
  <div class="container">
    <div class="card">
      <div class="content">
        <div class="payment-form">
          <div :class="activeTab === 1 ? 'payment-tab active':'payment-tab'" @click="() => this.activeTab = 1">
            <img src="@/assets/credit-card.png" alt="">
            <span class="payment-name"> Cartão de crédito </span>
          </div>
          <div :class="activeTab === 2 ? 'payment-tab active':'payment-tab'" @click="() => this.activeTab = 2">
            <img src="@/assets/pix.png" alt="">
            <span class="payment-name"> Pix </span>

          </div>
          <div :class="activeTab === 3 ? 'payment-tab active':'payment-tab'" @click="() => this.activeTab = 3">
            <img src="@/assets/boleto.png" alt="">
            <span class="payment-name"> Boleto </span>
          </div>
        </div>
        <div class="payment-content">
          <div class="content-tab" v-if="activeTab === 1">
            <div class="credit-card-container">
              <div class="card-input-container">
                <div class="input-container">
                  <span class="input-title"> Número do Cartão </span>
                  <input v-mask="cardMask" masked="false" class="input" v-model="this.cardNumber" type="text" name="Número do Cartão" id="card-number" placeholder="Digite somente os números">
                </div>
                <div class="input-container">
                  <span class="input-title"> Titular do Cartão </span>
                  <input class="input" v-model="this.cardName" type="text" name="Titular do Cartão" id="card-name" placeholder="Digite o nome impresso no cartão">
                </div>
                <div class="input-container">
                  <span class="input-title"> CPF/CNPJ do Titular </span>
                  <input v-mask="cpfCNPJMask" v-model="this.cpfCNPJCard" class="input" type="text" name="CPF/CNPJ do Titular" id="card-document" placeholder="Para emissão da nota fiscal">
                </div>
                <div class="security-container">
                  <div class="input-container">
                    <span class="input-title"> Validade </span>
                    <div class="select-container">
                      <select class="select" v-model="month_selected">
                        <option value="" disabled>Mês</option>
                        <option class="option" v-for="month in months" :value="month.value" :key="month.value">{{month.label}}</option>
                      </select>
                      <select class="select" v-model="year_selected">
                        <option value="" disabled>Ano</option>
                        <option class="option" v-for="year in years" :value="year.value" :key="year.value">{{year.label}}</option>
                      </select>
                    </div>
                  </div>
                  <div class="input-container">
                    <span class="input-title"> CVV </span>
                    <input v-mask="cvvMask" class="input" v-model="this.cvv" type="text" name="CVV" id="card-cvv" placeholder="CVV">
                  </div>
                </div>
                <div class="input-container">
                  <span class="input-title"> Número de Parcelas </span>
                  <div class="select-container">
                    <select class="select" v-model="installment_selected">
                      <option value="" disabled> Selecione número de parcelas </option>
                      <option class="option" v-for="installment in installments" :value="installment.value" :key="installment.value">{{installment.label}}</option>
                    </select>
                  </div>
                </div>
              </div>
              <div class="credit-card-img-container">
                <img class="credit-card-img" :src="creditCard" alt="">
              </div>
            </div>
          </div>
          <div class="content-tab" v-if="activeTab === 2">
            <div class="pix-container">
              <div class="pix-title-container">
                <span class="pix-title"> Libere sua compra rapidamente pagando com o Pix! </span>
              </div>
              <div class="pix-info-container">
                <div class="pix-row">
                  <div class="pix-box">
                    <div class="pix-image">
                      <img src="@/assets/clock.png" alt="">
                    </div>
                    <span class="pix-title-info">Rápida aprovação</span>
                    <span class="pix-subtitle-info">Pagamento em segundos, sem complicação.</span>
                  </div>
                  <div class="pix-box">
                    <div class="pix-image">
                      <img src="@/assets/qr-code.png" alt="">
                    </div>
                    <span class="pix-title-info">Facilidade na finalização</span>
                    <span class="pix-subtitle-info">Basta escanear, com o aplicativo do seu banco, o QRCode que iremos gerar para sua compra.</span>
                  </div>
                </div>
                <div class="pix-row">
                  <div class="pix-box">
                    <div class="pix-image">
                      <img src="@/assets/shield.png" alt="">
                    </div>
                    <span class="pix-title-info">Maior segurança</span>
                    <span class="pix-subtitle-info">O PIX foi desenvolvido pelo Banco Central para facilitar suas compras e é 100% seguro.</span>
                  </div>
                  <div class="pix-box">
                    <div class="pix-image">
                      <img src="@/assets/calendar.png" alt="">
                    </div>
                    <span class="pix-title-info">Tranquilidade na renovação</span>
                    <span class="pix-subtitle-info">A cada renovação da assinatura enviaremos um código PIX. Assim, você fica sempre em dia sem se preocupar.</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="content-tab" v-if="activeTab === 3">
            <div class="billet-container">
              <div class="billet-title-container">
                <span class="billet-title"> Atenção: </span>
              </div>
              <div class="billet-info-container">
                <div class="billet-row">
                  <div class="pix-box">
                    <div class="pix-image">
                      <img src="@/assets/clock.png" alt="">
                    </div>
                    <span class="pix-subtitle-info">Boletos levam até 3 dias úteis para serem compensados e então terem os produtos liberados.</span>
                  </div>
                  <div class="pix-box">
                    <div class="pix-image">
                      <img src="@/assets/mail.png" alt="">
                    </div>
                    <span class="pix-subtitle-info">Depois do pagamento, fique atento ao seu e-mail para receber os dados de acesso ao produto (verifique também a caixa de SPAM)</span>
                  </div>
                  <div class="pix-box">
                    <div class="pix-image">
                      <img src="@/assets/calendar.png" alt="">
                    </div>
                    <span class="pix-subtitle-info">A cada renovação da assinatura enviaremos um novo boleto para que você possa pagar. Assim, você fica sempre em dia sem se preocupar.</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="purchase-details">
          <div class="details-title-container">
            <span class="details-title">
              Detalhes da compra
            </span>
          </div>
          <div class="details">
            <span class="product-name"> Nome do Produto </span>
            <span class="product-price"> R$ 500,00 / mês </span>
          </div>
          <!-- <div class="charge">
            <img src="@/assets/credit-card-edit.png" alt="">
            <span class="charge-info">
              Essa cobrança aparecerá na sua fatura como: PAYT*NomeDoProduto
            </span>
          </div> -->
          <div class="pix-billet-container">
            <span class="cpf-cnpj-title"> CPF/CNPJ (Para emissão de Nota Fiscal) </span>
            <input v-mask="cpfCNPJMask" v-model="this.cpfCNPJ" class="input pix-billet-input" type="text" name="CPF/CNPJ" id="cpf-cnpj" placeholder="">
          </div>
        </div>
        <div class="buy-button-container">
          <button class="buy-button">Comprar Agora</button>
        </div>
        <div class="protection-img">
          <img src="@/assets/protection.png" alt="">
        </div>
      </div>
    </div>
  </div>
  
</template>

<script>
import {mask} from 'vue-the-mask'

export default {
  name: 'PaymentData',
  directives: {mask},
  props: {
  },
  data: function () {
    return {
      activeTab: 1,
      cardNumber: '',
      cardName: '',
      cpfCNPJCard: '',
      cpfCNPJ: '',
      cvv: '',
      cardMask: '################',
      cvvMask: '###',
      cpfCNPJMask: ['###.###.###-##', '##.###.###/####-##'],
      month_selected: '',
      year_selected: '',
      installment_selected: '',
      months: [
        {value: '1', label: 'Janeiro'},
        {value: '2', label: 'Fevereiro'},
        {value: '3', label: 'Março'},
        {value: '4', label: 'Abril'},
        {value: '5', label: 'Maio'},
        {value: '6', label: 'Junho'},
        {value: '7', label: 'Julho'},
        {value: '8', label: 'Agosto'},
        {value: '9', label: 'Setembro'},
        {value: '10', label: 'Outubro'},
        {value: '11', label: 'Novembro'},
        {value: '12', label: 'Dezembro'},
      ],
      years: [
        {value: '2023', label: '2023'},
        {value: '2024', label: '2024'},
        {value: '2025', label: '2025'},
        {value: '2026', label: '2026'},
        {value: '2027', label: '2027'},
        {value: '2028', label: '2028'},
        {value: '2029', label: '2029'},
        {value: '2030', label: '2030'},
        {value: '2031', label: '2031'},
        {value: '2032', label: '2032'},
        {value: '2033', label: '2033'},
        {value: '2034', label: '2034'},
      ],
      installments: [
      {value: '1', label: '1x de R$ 500,00'},
      {value: '1', label: '2x de R$ 250,00'},
      {value: '1', label: '3x de R$ 166,67'},
      {value: '1', label: '4x de R$ 125,00'},
      {value: '1', label: '5x de R$ 100,00'},
      ],
      visaCard: /^4[0-9]{15}$/,
      masterCard: /^(50|5[6-9]|6007|6220|6304|6703|6708|6759|676[1-3])|((5(([1-2]|[4-5])[0-9]{8}|0((1|6)([0-9]{7}))|3(0(4((0|[2-9])[0-9]{5})|([0-3]|[5-9])[0-9]{6})|[1-9][0-9]{7})))|((508116)\\d{4,10})|((502121)\\d{4,10})|((589916)\\d{4,10})|(2[0-9]{15})|(67[0-9]{14})|(506387)\\d{4,10})/,
      dinersCard: /^3(?:0[0-5]|[68][0-9])[0-9]{11}$/,
      amexCard: /^3[47][0-9]{13}$/,
      hiperCard: /^606282|^3841(?:[0|4|6]{1})0/,
      eloCard: /^4011(78|79)|^43(1274|8935)|^45(1416|7393|763(1|2))|^50(4175|6699|67[0-6][0-9]|677[0-8]|9[0-8][0-9]{2}|99[0-8][0-9]|999[0-9])|^627780|^63(6297|6368|6369)|^65(0(0(3([1-3]|[5-9])|4([0-9])|5[0-1])|4(0[5-9]|[1-3][0-9]|8[5-9]|9[0-9])|5([0-2][0-9]|3[0-8]|4[1-9]|[5-8][0-9]|9[0-8])|7(0[0-9]|1[0-8]|2[0-7])|9(0[1-9]|[1-6][0-9]|7[0-8]))|16(5[2-9]|[6-7][0-9])|50(0[0-9]|1[0-9]|2[1-9]|[3-4][0-9]|5[0-8]))/
    }
  },
  computed: {
    creditCard() {
      if(this.visaCard.test(this.cardNumber)){
        return require('@/assets/cardsTemplates/visa.png')
      } else if(this.masterCard.test(this.cardNumber)) {
        return require('@/assets/cardsTemplates/mastercard.png')
      } else if (this.dinersCard.test(this.cardNumber)) {
        return require('@/assets/cardsTemplates/diners.png')
      } else if (this.amexCard.test(this.cardNumber)) {
        return require('@/assets/cardsTemplates/amex.png')
      } else if(this.hiperCard.test(this.cardNumber)) {
        return require('@/assets/cardsTemplates/hipercard.png')
      } else if(this.eloCard.test(this.cardNumber)){
        return require('@/assets/cardsTemplates/elo.png')
      } else {
        return require('@/assets/cardsTemplates/default.png')
      }
    }
  },
  methods: {
    cpfCnpjValidation: (cpfCnpj) => {
      // eslint-disable-next-line no-useless-escape
      const cpfCnpjCheck =  /(^\d{3}\.\d{3}\.\d{3}\-\d{2}$)|(^\d{2}\.\d{3}\.\d{3}\/\d{4}\-\d{2}$)/;
      if (cpfCnpj.match(cpfCnpjCheck)) {
        return true; 
      } 
      return false; 
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  margin-bottom: 16px;
}

.pix-billet-input {
  width: 55%;
  box-sizing: border-box;
}

.pix-billet-container {
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
  flex-direction: column;
  width: 100%;
  margin-bottom: 16px;
}

.cpf-cnpj-title {
  font-size: 12px;
  font-weight: 400;
  line-height: 21px;
  letter-spacing: 0em;
  text-align: left;
  color: #000000;
}

.pix-container, .billet-container {
  display: flex;
  flex-direction: column;
  width: 100%;
}
.pix-title-container, .pix-info-container, .billet-info-container {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
}
.billet-title-container {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  width: 100%;
}
.billet-title {
  font-size: 16px;
  font-weight: 400;
  line-height: 24px;
  letter-spacing: 0em;
  text-align: left;
  color: #707070;
}

.pix-info-container, .billet-info-container {
  flex-direction: column;
  row-gap: 16px;
}

.billet-info-container {
  margin-bottom: 16px;
}

.pix-row {
  display: grid;
  grid-template-columns: 5fr 5fr;
  align-items: center;
  justify-content: center;
  gap: 12px;
}
.billet-row {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(208px, 1fr));
  align-items: center;
  justify-content: center;
  gap: 12px;
}

.pix-box{
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  padding: 8px;
  border-radius: 8px;
  border: 1px solid #B0B0B0;
  gap: 12px;
  min-height: -webkit-fill-available;
}

.pix-title-info {
  font-size: 14px;
  font-weight: 600;
  line-height: 17px;
  letter-spacing: 0em;
  text-align: center;
  color: #212529;
}

.pix-subtitle-info {
  font-size: 12px;
  font-weight: 400;
  line-height: 15px;
  letter-spacing: 0em;
  text-align: center;
  color: #212529;
}

.pix-title {
  font-size: 16px;
  font-weight: 400;
  line-height: 24px;
  letter-spacing: 0em;
  text-align: left;
  color: #707070;
}

.payment-form {
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  flex-direction: row;
  flex-flow: wrap;
  gap: 24px;
  margin-bottom: 32px;
}

.payment-tab {
  width: 132px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #B0B0B0;
  gap: 10px;
  cursor: pointer;
  min-height: 40px;
}

.payment-tab.active {
  background: rgba(255, 105, 5, .1);
  border: 1px solid #FF6905;
}

.payment-name {
  width: 61px;
  font-size: 12px;
  font-weight: 500;
  line-height: 15px;
  letter-spacing: 0em;
  text-align: left;
  color: #8E939A;
}

.content-tab {
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  flex-direction: column;
  gap: 8px;
  margin-bottom: 16px;
}

.input-container {
  display: flex;
  align-items: flex-start;
  justify-content: center;
  flex-direction: column;
  width: 100%;
}

.select {
  min-width: 80px;
  height: 40px;
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #CED4DA;
  cursor: pointer;
  width: 100%;
}

.select-container{
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
  flex-direction: row;
  width: 100%;
  gap: 10px;
}

.card-input-container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap: 8px;
}

.security-container {
  display: flex;
  width: 100%;
  gap: 15px;
}

.credit-card-container {
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  flex-direction: row;
  gap: 24px;
  width: 100%;
}

.credit-card-img-container {
  display: flex;
  align-items: center;
  justify-content: center;
}

.credit-card-img {
  width: 100%;
  height: 100%;
}

.details-title {
  font-size: 14px;
  font-weight: 400;
  line-height: 21px;
  letter-spacing: 0em;
  text-align: left;
  color: #000000;
}

.details {
  display: flex;
  align-items: center;
  justify-content: space-between;
  text-align: center;
  margin-bottom: 8px;
}

.details-title-container {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  text-align: center;
  margin-bottom: 8px;
}

.charge {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  text-align: center;
  margin-bottom: 8px;
  gap: 8px;
}

.charge-info {
  font-size: 10px;
  font-weight: 400;
  line-height: 21px;
  letter-spacing: 0em;
  text-align: left;
}

.product-name {
  font-size: 12px;
  font-weight: 700;
  line-height: 15px;
  letter-spacing: 0em;
  text-align: left;
  color: #303133;
}

.product-price {
  font-size: 12px;
  font-weight: 400;
  line-height: 15px;
  letter-spacing: 0em;
  text-align: left;
  color: #303133;
}

.buy-button-container {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  text-align: center;
  margin-bottom: 8px;
}

.buy-button {
  width: 360px;
  height: 56px;
  padding: 16px 32px 16px 32px;
  border-radius: 4px;
  border: 1px solid #F6A13C;
  background: linear-gradient(0deg, #FF6905, #FF6905);
  font-size: 18px;
  font-weight: 500;
  line-height: 24px;
  letter-spacing: 0em;
  text-align: center;
  color: #FFFFFF;
  cursor: pointer;
}
</style>
