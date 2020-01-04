<template>
  <main>
      <h1 id="heading" class="text">Ledger</h1>
      <div class="ledger-item">
          <span class="text">Current Total</span>
          <span class="text">${{currentTotal}}</span>
      </div>
      <div id="completed-bills">
          <ul id="ledger-list">
              <li v-for="bill in bills" :key="bill.name">
                  <div class="ledger-item">
                      <span class="text bill-name">{{bill.name}}</span>
                      <span class="text bill-value">-${{bill.value}}</span>
                  </div>
              </li>
          </ul>
      </div>
  </main>
</template>

<script>
export default {
    name: 'Ledger',
    props:{
        bills: {
            type: Array
        },
        currentTotal: {
            type: Number
        }
    },
    data() {
        return {
            
        }
    },
    computed: {
        getCurrentTotal() {
            let currentTotal = this.currentTotal;
            for(const bill of this.bills){
                if (bill.complete){
                    currentTotal -= bill.value;
                }
            }
            return currentTotal;
        }
    }
}
</script>

<style>
main{
    display: grid;
}
.ledger-item{
    display: flex;
    justify-content: space-between;
    width: 50vw;
    padding: 0px;
}
#ledger-list{
    margin-top: 5rem; 
    list-style-type: none;
}
.bill-value{
    color: red;
}
input#currentTotal:focus{
    outline: none;
}
</style>