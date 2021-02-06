<template>
  <button :disabled="disabled" @click="action">{{ text }}</button>
</template>

<script>
export default {
  name: "BalanceActions",
  props: {
    text: String,
    disabled: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    action() {
      this.$emit("action");
    },
  },
};
</script>

<style></style>
