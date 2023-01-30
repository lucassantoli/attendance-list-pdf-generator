<template>
  <button
    :class="{ 'dark': dark }"
    @click="$emit('click')"
  >
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "ButtonComponent",

  props: {
    dark: Boolean
  }
}
</script>

<style lang="scss">
@import "@/styles/variables.scss";

button {
  padding: .75rem;
  color: $background;
  background-color: $text;
  border-radius: .25rem;
  font-size: 1rem;
  font-weight: 700;
  font-family: 'Inter', sans-serif;
  border: none;
  outline: 0;

  &.dark {
    background-color: $background;
    color: $text;
  }

  &.pink   { background-color: $pink; }
  &.cyan   { background-color: $cyan; }
  &.orange { background-color: $orange; }  
}
</style>