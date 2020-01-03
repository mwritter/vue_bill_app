<template>
  <div id="app">
    <app-bill-checklist :bills="this.getBills()" />
  </div>
</template>

<script>
import BillChecklist from './components/BillChecklist'

export default {
  name: 'app',
  components: {
    'app-bill-checklist': BillChecklist
  },
  data(){
    return {
      bills: [
        {name:'Rent', value:535},
        {name:'Mediacom', value: 65},
        {name:'Student Loan' , value: 460},
        {name:'Utility', value: 95},
        {name:'Phone', value: 181},
        {name:'Toyota', value: 216},
        {name:'Nission', value: 245},
        {name:'Car insurance', value: 195}
      ]
    }
  },
  methods: {
    getBills() {
      return this.bills;
    }
  }
}
</script>

<style>
#app {
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
</style>
