<template>
  <h1 class="greeting">Hello {{ name }}</h1>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: { name: { type: String, required: true } }
}
</script>

<style scoped>
.greeting {
  color:#008000;
  font-family: Georgia, "Times New Roman", serif;
  font-weight: 700;
  font-size: 2.6rem;
  margin: 0 0 .35rem 0;
}
</style>
