<template>
  <main>
      <div class="container">
        <h1 id="heading" class="text">Ledger</h1>
        <div class="ledger-item">
            <span class="text">Current Total</span>
            <span class="text">${{this.getCurrentTotal}}</span>
        </div>
        <div id="completed-bills">
            <ul id="ledger-list" class="text">
                <li class="ledger-item" v-for="bill in bills" :key="bill.name">
                    <span class="bill-name">{{bill.name}}</span>
                    <span class="bill-value">-${{bill.value}}</span>
                </li>
                <li class="ledger-item" v-if="miscs.length > 0">
                    <span class="bill-name">Miscellaneous</span>
                    <span class="bill-value">-${{this.getCurrentMiscTotal}}</span>
                </li>
            </ul>
        </div>
      </div>
  </main>
</template>

<script>
export default {
    name: 'Ledger',
    props:{
        miscs: {
            type: Array
        },
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
            const ledgerItems = [...this.bills, ...this.miscs]
            for(const bill of ledgerItems){
                if (bill.complete){
                    currentTotal -= bill.value;
                }
            }
            return currentTotal;
        },
        getCurrentMiscTotal() {
            let total = 0;
            for(const misc of this.miscs){
                total += misc.value;
            }
            return total;
        }
    }
}
</script>

<style>
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

</style>