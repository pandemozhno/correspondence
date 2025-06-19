<script setup>
  const {
    items
  } = defineProps({
    items: {
      type: [Array, Object],
      default: () => []
    }
  })

  const selected = defineModel('selected');

</script>

<template>
  <div class="c-list">
    <div
      :class="['c-list__option', { 'c-list__option_selected': selected === key }]"
      v-for="option, key in items"
      @click="selected = key"
    >
      {{ key }} {{ option }}
    </div>
  </div>
</template>

<style scoped>
.c-list {
  background-color: #f9f9f9;
  padding: 1rem;
  display: flex;
  
}

.c-list__option {
  padding: .4rem;
  color: var(--vt-c-indigo);
  background: var(--vt-c-text-dark-2);
  cursor: pointer;
  margin: .5rem;
}

.c-list__option_selected {
  color: var(--vt-c-white-soft);
  background: var(--vt-c-indigo);
    
}
</style>
