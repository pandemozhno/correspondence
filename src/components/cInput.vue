<script setup>
const model = defineModel()

</script>
<template>
  <input class="c-input" type="text" v-model="model"/>
</template>

<style scoped>
.c-input {
  border: 0;
  background: var(--vt-c-white-soft);
  padding: .8rem;
  border-radius: .2rem;
}
</style>
