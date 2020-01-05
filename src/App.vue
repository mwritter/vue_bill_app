<template>
  <div id="app">
    <div id="controls">
      <label for="current-total">Current Total</label>
      <input id="currentTotal" name="current-total" v-model="currentTotal" type="number" />
    </div>
    <div id="components">
      <app-bill-checklist @toggleBill="toggleBill" :bills="this.getBills()" />
      <app-ledger
        :miscs="this.getMisc"
        :bills="this.getCompletedBills"
        :currentTotal="this.getCurrentTotal"
      />
      <app-misc @addMisc="addMisc" :miscs="this.getMisc"></app-misc>
    </div>
  </div>
</template>

<script>
import BillChecklist from "./components/BillChecklist";
import Ledger from "./components/Ledger";
import Misc from "./components/Misc";

export default {
  name: "app",
  components: {
    "app-bill-checklist": BillChecklist,
    "app-ledger": Ledger,
    "app-misc": Misc
  },
  data() {
    return {
      currentTotal: 0,
      bills: [
        { name: "Rent", value: 535.0, complete: false },
        { name: "Mediacom", value: 65.0, complete: false },
        { name: "Gas", value: 25.0, complete: false },
        { name: "Student Loan", value: 460.0, complete: false },
        { name: "Utility", value: 95.0, complete: false },
        { name: "Phone", value: 181.0, complete: false },
        { name: "Toyota", value: 216.0, complete: false },
        { name: "Nission", value: 245.0, complete: false },
        { name: "Car insurance", value: 195.0, complete: false },
        { name: "Gym", value: 20.0, complete: false }
      ],
      miscs: []
    };
  },
  computed: {
    getCompletedBills() {
      const completed = this.bills.filter(bill => {
        return bill.complete;
      });
      return completed;
    },
    getMisc() {
      return this.miscs;
    },
    getCurrentTotal() {
      return parseFloat(this.currentTotal);
    }
  },
  methods: {
    getBills() {
      return this.bills;
    },
    toggleBill(bill) {
      bill.complete = !bill.complete;
      this.currentTotal = parseFloat(this.currentTotal);
      // after toggle
      if (bill.complete) {
        this.currentTotal -= parseFloat(bill.value);
      } else {
        this.currentTotal += parseFloat(bill.value);
      }
    },
    addMisc(misc) {
      this.miscs = misc ? [...this.miscs, misc] : this.misc;
    }
  }
};
</script>

<style>
* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}
#app {
  display: gird;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#components {
  display: grid;
  align-content: start;
  grid-template-columns: 1fr 1fr 1fr;
}
main {
  display: flex;
  justify-content: center;
}
.container {
  display: grid;
  height: 100vh;
  width: 75%;
  align-content: start;
}
#heading {
  transform: rotate(-6deg);
  background-color: #e7dab6;
  width: 55%;
  height: 35px;
  justify-self: center;
  margin-bottom: 2rem;
}
.text {
  font-family: "Caveat", cursive;
  font-size: 1.5em;
}
#controls {
  margin-bottom: 30px;
}
#controls #currentTotal {
  max-width: 100px;
  font-size: 1.2em;
  margin-left: 10px;
}
.add-btn {
  display: flex;
  font-size: 1em;
  justify-content: center;
  align-items: center;
  justify-self: end;
  cursor: pointer;
  background: white;
  color: black;
  width: 3em;
  height: 3em;
  border-radius: 50%;
  border: 1px solid black;
}
</style>
