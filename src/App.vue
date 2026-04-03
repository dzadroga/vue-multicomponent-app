<template>
  <div class="page">
    <HelloWorld :name="name" />

    <p class="account-info">
      Account Balance: {{ balance }} {{ abbr(from) }}, Amount: {{ amount }} {{ abbr(from) }}
    </p>

    <Balance
      :balance="balance"
      :amount="amount"
      :denomination="from"
      @update:amount="amount = $event"
      @update:balance="balance = $event"
    />

    <Currency
      :amount="amount"
      :from="from"
      :to="to"
      @update:from="from = $event"
      @update:to="to = $event"
    />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Balance from './components/Balance.vue'
import Currency from './components/Currency.vue'

export default {
  name: 'App',
  components: { HelloWorld, Balance, Currency },
  data() {
    return {
      name: 'Dakota',
      balance: 55,
      amount: 30,
      from: 'US Dollar',
      to: 'Indian Rupee'
    }
  },
  methods: {
    abbr(x) {
      const m = { 'US Dollar':'USD','Indian Rupee':'INR','Bahraini Dinar':'BHD','Euro':'EUR' }
      return m[x] || x
    }
  }
}
</script>

<style scoped>
.page { padding: 12px 16px; }

.account-info {
  font-family: Georgia, "Times New Roman", serif;
  font-weight: 700;
  margin: 0 0 10px 0;
}
</style>
