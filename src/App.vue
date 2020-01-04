<template>
  <div id="app">
    <div id="controls">
      <label for="current-total">Current Total</label>
      <input id="currentTotal" name="current-total" v-model="currentTotal" type="number">
    </div>
    <app-bill-checklist @toggleBill="toggleBill" :bills="this.getBills()" />
    <app-ledger :miscs="this.getMisc" :bills="this.getCompletedBills" :currentTotal="this.getCurrentTotal()"/>
    <app-misc :miscs="this.getMisc" ></app-misc>
  </div>
</template>

<script>
import BillChecklist from './components/BillChecklist'
import Ledger from './components/Ledger'
import Misc from './components/Misc'

export default {
  name: 'app',
  components: {
    'app-bill-checklist': BillChecklist,
    'app-ledger': Ledger,
    'app-misc': Misc
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
      ],
      miscs: [
        {name: 'Smoothies', value: 10.00, id: 1, complete: true},
        {name: 'Smoothies', value: 10.00, id: 2, complete: true}

      ]
    }
  },
  computed: {
    getCompletedBills(){
      const completed = this.bills.filter(bill => {
        return bill.complete
      })
      return completed
    },
    getMisc(){
      return this.miscs;
    },
  },
  methods: {
    getBills() {
      return this.bills;
    },
    getCurrentTotal(){
      return parseFloat(this.currentTotal);
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
main{
    display: flex;
    justify-content: center;
}
.container{
    display: grid;
}
#heading{
    transform: rotate(-6deg);
    background-color: #E7DAB6;
    width: 30%;
    justify-self: center;
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
