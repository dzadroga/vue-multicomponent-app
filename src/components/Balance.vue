<template>
  <div class="balance">
    <label class="slider-label">Change amount to:</label>
    <input
      class="slider"
      type="range"
      min="5"
      max="100"
      step="5"
      :value="amount"
      @input="$emit('update:amount', +$event.target.value)"
    />

    <div class="denom">
      Balance shown in {{ denomination }}
    </div>

    <div class="buttons">
      <button class="btn" @click="add">Add</button>
      <button class="btn" @click="subtract" :disabled="amount > balance">Subtract</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Balance',
  props: {
    balance: { type: Number, required: true },
    amount: { type: Number, required: true },
    denomination: { type: String, required: true }
  },
  methods: {
    add() {
      this.$emit('update:balance', this.balance + this.amount)
    },
    subtract() {
      if (this.amount <= this.balance) {
        this.$emit('update:balance', this.balance - this.amount)
      }
    }
  }
}
</script>

<style scoped>
.slider-label {
  display: block;
  margin: 10px 0 6px 0;
  font-family: Georgia, "Times New Roman", serif;
  font-size: 0.95rem;
}
.slider {
  width: 420px;
  margin-bottom: 10px;
}
.buttons { margin-top: 6px; }
.btn {
  font-size: .9rem;
  padding: 4px 10px;
  margin-right: 8px;
  background: #eee;
  border: 1px solid #bbb;
  border-radius: 3px;
  cursor: pointer;
}
.btn:disabled {
  opacity: .6;
  cursor: not-allowed;
}
</style>
