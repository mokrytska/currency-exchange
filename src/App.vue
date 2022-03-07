<template>
  <fragment>
    <div class="wrapper">
      <input v-model="sourceAmount" type="number" class="border"/>
      <select
        class="select border"
        name="select"
        v-model="sourceCurrency"
        @change="countOutputAmount"
      >
        <option v-for="item in currencyItems" v-bind:key="item">
          {{ item }}
        </option>
      </select>
      <input type="number" v-model="outputAmount" class="border"/>
      <select
        class="select border"
        name="select"
        v-model="outputCurrency"
        @change="countSourceAmount"
      >
        <option v-for="item in currencyItems" v-bind:key="item">
          {{ item }}
        </option>
      </select>
    </div>
  </fragment>
</template>

<script>
export default {
  data() {
    return {
      sourceAmount: '0',
      sourceCurrency: '',
      outputAmount: '0',
      outputCurrency: '',
      currency: {},
      currencyItems: [],
    };
  },
  methods: {
    async getData() {
      let response = await fetch(
        'https://freecurrencyapi.net/api/v2/latest?apikey=9F9ek9MUGlgme5ZL0aXF4uPvcfMeldaeyJs1HNWO', {mode: 'no-cors'}
      );
      let json = await response.json();
      this.currency = json.data;
      console.log(Object.keys(this.currency));
      this.currencyItems = Object.keys(this.currency);
      this.sourceCurrency = this.currencyItems[138];
      this.outputCurrency = this.currencyItems[45];
      console.log(this.currencyItems.sort());
      return json;
    },

    countSourceAmount() {
      const sourceCurrencyValue = this.currency[this.sourceCurrency];
      const outputCurrencyValue = this.currency[this.outputCurrency];

      this.outputAmount = (
        this.sourceAmount /
        (sourceCurrencyValue / outputCurrencyValue)
      ).toFixed(2);
      console.log(this.outputAmount);
    },

    countOutputAmount() {
      const sourceCurrencyValue = this.currency[this.sourceCurrency];
      const outputCurrencyValue = this.currency[this.outputCurrency];

      this.sourceAmount = (
        this.outputAmount *
        (sourceCurrencyValue / outputCurrencyValue)
      ).toFixed(2);
      console.log(this.sourceAmount);
    },
  },

  mounted() {
    this.getData();
  },
};
</script>

<style>
.wrapper {
  display: grid;
  grid-template-columns: 200px 200px;
  grid-column-gap: 10px;
  grid-row-gap: 1em;
}
.select {
  width: 100px;
  padding-bottom: 10px;
  text-align: center;
  display: flex;
  align-items: center;
  line-height: 30px;
}
.button {
  margin-top: 10px;
}
.border {
  border-radius: 5px;
  border: solid 2px gray;
}
</style>
