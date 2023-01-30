<template>
  <span class="indicator">
    <slot></slot>
  </span>
</template>

<script>
export default {
  name: "StepIndicator",
}
</script>

<style lang="scss">
@import "@/styles/variables.scss";

.indicator {
  margin: {
    left: auto;
    right: auto;
  }
  --dimensions: 1.6rem;
  font-size: 1rem;
  height: var(--dimensions);
  width: var(--dimensions);
  font-weight: 700;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: $background;
  color: $text;
  border-radius: 50%;

  &.dark {
    background-color: $text;
    color: $background;
  }

  &.pink   { background-color: $pink; }
  &.cyan   { background-color: $cyan; }
  &.orange { background-color: $orange; }
}
</style>