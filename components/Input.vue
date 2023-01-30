<template>
  <input type="text" v-model="inputVal" v-bind="$attrs">
</template>

<script>
export default {
  name: "InputComponent",

  props: {
    value: [Number, String, Object],
  },

  computed: {
    inputVal: {
      get: function() {
        return this.value;
      },
      set: function(value) {
        this.$emit('input', value);
      }
    }
  }
}
</script>

<style lang="scss">
@import "@/styles/variables.scss";

input {
  outline: 0;
  border: 1px solid $light-gray-1;
  background: transparent;
  padding: .75rem;
  color: $text;
  border-radius: .25rem;
  font-size: 1rem;
}
</style>