<template>
  <div id="app">
    <div id="controls">
      <label for="current-total">Current Total</label>
      <input id="currentTotal" name="current-total" v-model="currentTotal" type="number">
    </div>
    <app-bill-checklist @toggleBill="toggleBill" :bills="this.getBills()" />
    <app-ledger :bills="this.getCompletedBills" :currentTotal="this.getCurrentTotal()"/>
  </div>
</template>

<script>
import BillChecklist from './components/BillChecklist'
import Ledger from './components/Ledger'

export default {
  name: 'app',
  components: {
    'app-bill-checklist': BillChecklist,
    'app-ledger': Ledger
  },
  data(){
    return {
      currentTotal: 0,
      bills: [
        {name:'Rent', value: 535.00, complete: false},
        {name:'Mediacom', value: 65.00, complete: false},
        {name:'Student Loan' , value: 460.00, complete: false},
        {name:'Utility', value: 95.00, complete: false},
        {name:'Phone', value: 181.00, complete: false},
        {name:'Toyota', value: 216.00, complete: false},
        {name:'Nission', value: 245.00, complete: false},
        {name:'Car insurance', value: 195.00, complete: false}
      ]
    }
  },
  computed: {
    getCompletedBills(){
      return this.bills.filter(bill => {
        return bill.complete;
      })
    }
  },
  methods: {
    getBills() {
      return this.bills;
    },
    getCurrentTotal(){
      return this.currentTotal;
    },
    toggleBill(bill){
      bill.complete = !bill.complete;
      // after toggle
      if (bill.complete){
        this.currentTotal -= parseFloat(bill.value)
      } else {
        this.currentTotal += parseFloat(bill.value)
      }
    },
  }
}
</script>

<style>
* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}
#app {
  display: gird;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.text{
  font-family: 'Caveat', cursive;
  font-size: 1.5em;
}
#controls {
  margin-bottom: 30px;
}
#controls #currentTotal{
  max-width: 100px;
  font-size: 1.2em;
  margin-left: 10px;
}
</style>
