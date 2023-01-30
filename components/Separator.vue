<template>
  <div class="separator">
    <div class="separator-content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style lang="scss">
@import "@/styles/variables.scss";

.separator {
  position: relative;
  --border-width: 1px;
  margin-bottom: 2rem;

  .separator-content {
    text-align: center;
    width: max-content;
    background-color: $background;
    border: var(--border-width) solid $light-gray-1;
    color: $light-gray-1;
    padding: .5rem 1.5rem;
    border-radius: 200px;
    margin: {
      left: auto;
      right: auto;
    }
  }
  
  &::before {
    content: '';
    position: absolute;
    left: 0;
    right: 0;
    top: 50%;
    transform: translateY(-0.5px);
    height: var(--border-width);
    background-color: $light-gray-1;
    z-index: -1;
  }
}
</style>