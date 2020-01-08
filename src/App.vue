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
      <app-misc
        :currentTotal="this.getCurrentTotal"
        @addMisc="addMisc"
        @deleteMisc="deleteMisc"
        :miscs="this.getMisc"
      ></app-misc>
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
      miscs: [],
      totalPaid: 0
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
      return parseFloat(this.currentTotal) - parseFloat(this.totalPaid);
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
        this.totalPaid += bill.value;
      } else {
        this.totalPaid -= bill.value;
      }
    },
    addMisc(misc) {
      this.miscs = misc ? [...this.miscs, misc] : this.misc;
      this.totalPaid += misc ? misc.value : 0;
    },
    deleteMisc(misc) {
      this.miscs = this.miscs.filter(item => {
        return item.id != misc.id;
      });
      this.totalPaid -= misc.value;
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
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  /* border: 1px solid black; */
}
#components {
  display: grid;
  align-content: start;
  grid-template-columns: 1fr 1fr 1fr;
}
main {
  display: flex;
  justify-content: center;
  align-content: start;
  height: 75vh;
  /* border: 1px solid blue; */
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 75%;
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
#add-section {
  display: grid;
  justify-content: end;
}
.action-btn {
  display: flex;
  font-size: 1em;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  background: white;
  color: black;
  width: 3em;
  height: 3em;
  border-radius: 50%;
  border: 1px solid black;
}
.checkbox {
  margin: 0.5rem;
}
</style>
