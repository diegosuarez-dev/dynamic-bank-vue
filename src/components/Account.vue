<template>
  <h2>Account type: {{ type }}</h2>
  <h2>Balance: {{ balance }}</h2>
  <h3>Account status: {{ state ? "active" : "inactive" }}</h3>
  <h3>Available services:</h3>
  <div v-for="(item, index) in services" :key="index">{{ item }}</div>
  <BalanceActions text="Add to balance" @action="add" />
  <BalanceActions
    :disabled="disabled"
    text="Subtract from balance"
    @action="subtract"
  />
</template>

<script>
import BalanceActions from "./BalanceActions";

export default {
  name: "Account",
  components: {
    BalanceActions,
  },
  data() {
    return {
      type: "current",
      balance: 1000,
      state: true,
      services: ["transferences", "payments", "checks"],
      disabled: false,
    };
  },
  methods: {
    add() {
      this.balance += 100;
      if (this.balance >= 100) this.disabled = false;
    },
    subtract() {
      if (this.balance === 100) {
        let answer = confirm(
          "You will be out of cash. Are you sure to proceed?"
        );
        if (answer) {
          this.balance -= 100;
          this.disabled = true;
        }
      } else if (this.balance > 100) {
        this.balance -= 100;
      } else {
        alert("You don't have enough money for that");
      }
    },
  },
};
</script>

<style></style>
