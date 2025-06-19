<template>
  <button class="c-button">
    <slot />
  </button>
</template>

<style scoped>
.c-button {
  background-color: var(--vt-c-indigo);
  color: var(--vt-c-white-soft);
  cursor: pointer;
  border: none;
  border-radius: .3rem;
  padding: .8rem;
  border: 0;
}
</style>
