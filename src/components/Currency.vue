<template>
  <div class="converter">
    <h3>Currency Converter</h3>

    <div class="form-row">
      <label for="enterAmount">Enter Amount:</label>
      <input
        id="enterAmount"
        type="number"
        v-model.number="localAmount"
      />
    </div>

    <div class="form-row">
      <label for="convertFrom">Convert From:</label>
      <select :value="localFrom" @change="updateFrom($event)">
        <option>US Dollar</option>
        <option>Indian Rupee</option>
        <option>Bahraini Dinar</option>
        <option>Euro</option>
      </select>

      <span class="spacer">Convert To:</span>
      <select :value="localTo" @change="updateTo($event)">
        <option>Indian Rupee</option>
        <option>US Dollar</option>
        <option>Bahraini Dinar</option>
        <option>Euro</option>
      </select>
    </div>

    <p class="result">
      {{ localAmount }} {{ fromAbbr }} equals {{ converted }} {{ toAbbr }}
    </p>
  </div>
</template>

<script>
export default {
  name: 'Currency',
  props: {
    amount: { type: Number, required: true },
    from:   { type: String, required: true },
    to:     { type: String, required: true }
  },
  data() {
    return {
      localAmount: this.amount,
      localFrom: this.from,
      localTo: this.to
    }
  },
  watch: {
    amount(newVal) {
      this.localAmount = newVal  
    }
  },
  methods: {
    updateFrom(event) {
      this.localFrom = event.target.value
      this.$emit('update:from', this.localFrom)   
    },
    updateTo(event) {
      this.localTo = event.target.value
      this.$emit('update:to', this.localTo)       
    }
  },
  computed: {
    usdPer() {
      return {
        'US Dollar': 1, // based on exchange rates posted on 9.10.2025
        'Indian Rupee': 0.011,
        'Bahraini Dinar': 2.65,
        'Euro': 1.17
      }
    },
    abbrMap() {
      return {
        'US Dollar': 'USD',
        'Indian Rupee': 'INR',
        'Bahraini Dinar': 'BHD',
        'Euro': 'EUR'
      }
    },
    converted() {
      const usd = this.localAmount * (this.usdPer[this.localFrom] ?? 1)
      const out = usd / (this.usdPer[this.localTo] ?? 1)
      return out.toFixed(1)
    },
    fromAbbr() { return this.abbrMap[this.localFrom] ?? this.localFrom },
    toAbbr()   { return this.abbrMap[this.localTo] ?? this.localTo }
  }
}
</script>

<style scoped>
.converter { background:#ddd; padding:16px; margin-top:12px; max-width:760px;
  font-family:"Times New Roman",serif; font-size:1rem; }
h3 { font-family:Georgia,"Times New Roman",serif; font-weight:700; margin:0 0 12px; font-size:1.3rem; }
.form-row { display:flex; align-items:center; margin-bottom:12px; }
.form-row label { width:130px; font-family:"Times New Roman",serif; }
.form-row input[type="number"] { font-family:"Courier New",monospace; font-size:1rem; padding:2px 5px; width:360px; }
.form-row select { font-family:"Courier New",monospace; font-size:1rem; padding:2px 5px; height:28px; width:200px; margin-right:14px; }
.spacer { margin:0 6px; }
.result { margin-top:0; }
</style>