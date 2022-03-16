<template>
  <div>
    <div class="wrapper">
      <input
        v-model="sourceAmount"
        type="number"
        class="border"
        @input="countSourceAmount"
      />
      <Select
        :currency-items="currencyItems"
        v-model="sourceCurrency"
        @change="countSourceAmount()"
      ></Select>
      <input
        type="number"
        v-model="outputAmount"
        class="border"
        @input="countOutputAmount"
      />
      <Select
        :currency-items="currencyItems"
        v-model="outputCurrency"
        @change="countSourceAmount()"
      ></Select>
      
      <Switcher v-model="switcher"></Switcher>
    </div>
  </div>
</template>

<script>
import Select from './components/currency-select.vue';
import Switcher from './components/switcher.vue';
export default {
  components: {
    Select, 
    Switcher,
  },
  data() {
    return {
      sourceAmount: '0',
      sourceCurrency: '',
      outputAmount: '0',
      outputCurrency: '',
      currencies: {},
      currencyItems: [],
      switcher: false,
    };
  },
  methods: {
    async getData() {
      let response = await fetch(
        'http://data.fixer.io/api/latest?access_key=11e4592285b7d86b6edf95bc4a91dcbf'
      );
      let json = await response.json();
      console.log(json);
      this.currencies = json.rates;
      console.log(Object.keys(this.currencies));
      this.currencyItems = Object.keys(this.currencies);
      console.log(this.currencyItems[40]);
      console.log(this.currencyItems.sort());
      return json;
    },

    countSourceAmount() {
      const sourceCurrencyValue = this.currencies[this.sourceCurrency];
      const outputCurrencyValue = this.currencies[this.outputCurrency];

      this.outputAmount = (
        this.sourceAmount /
        (sourceCurrencyValue / outputCurrencyValue)
      ).toFixed(2);
      console.log(this.outputAmount);
    },

    countOutputAmount() {
      const sourceCurrencyValue = this.currencies[this.sourceCurrency];
      const outputCurrencyValue = this.currencies[this.outputCurrency];

      this.sourceAmount = (
        this.outputAmount *
        (sourceCurrencyValue / outputCurrencyValue)
      ).toFixed(2);
      console.log(this.sourceAmount);
    },
  },
  mounted() {
    this.getData();
    this.getItems();
    console.log(this.sourceCurrency);
  },
};
</script>

<style>
.wrapper {
  display: grid;
  grid-template-columns: 200px 200px;
  grid-gap: 10px;
}

.border {
  border-radius: 5px;
  border: solid 2px gray;
}

</style>
