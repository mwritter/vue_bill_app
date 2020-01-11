<template>
  <main>
    <div class="container">
      <div>
        <h1 id="heading" class="text">Ledger</h1>
        <div class="ledger-item">
          <span class="text">Current Total</span>
          <span class="text">${{parseFloat(currentTotal) + getPaymentTotal}}</span>
        </div>
        <div id="completed-bills">
          <ul id="ledger-list" class="text">
            <li class="ledger-item" v-for="(item, index) in getCompleted" :key="index">
              <span class="bill-name">{{item.name}}</span>
              <span :class="{'payment': item.type == 'payment'}" class="bill-value">-${{item.value}}</span>
            </li>
            <li class="ledger-item" v-if="this.miscTotal > 0">
              <span class="bill-name">Miscellaneous</span>
              <span class="bill-value">-${{this.miscTotal}}</span>
            </li>
          </ul>
        </div>
        <form v-if="this.adding" id="new-ledger-form" @submit.prevent>
            <div id="form-inputs">
              <input
                class="text"
                placeholder="Description"
                id="item-name"
                type="text"
              />
              <input
                class="text"
                placeholder="Pay"
                step="0.01"
                min="1"
                id="item-value"
                type="number"
              />
            </div>

            <div class="action-section">
              <button
                class="action-btn small-btn small-success-btn"
                title="Submit Pay"
                @click="submitAdd()"
              ></button>
              <button
                class="action-btn small-btn small-danger-btn"
                title="Cancel"
                @click="cancelAdd()"
              ></button>
            </div>
          </form>
      </div>
       <div id="add-section">
        <div @click="adding = true" title="Add Misc Item" class="action-btn add-btn" id="add-misc">+</div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "Ledger",
  props: {
    miscTotal: {
      type: Number
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
      adding: false,
      payments: [
        
      ]
    };
  },
  computed: {
    getPayments(){
      return this.payments;
    },
    getPaymentTotal(){
      return this.getPayments.reduce((total, payment) => {
        return total + parseFloat(payment.value)
      }, 0)
    },
    getCompleted(){
      return [...this.bills, ...this.getPayments]
    }
  },
  methods: {
    cancelAdd(){
      this.adding = false;
    },
    submitAdd(){
      const form = document.getElementById('new-ledger-form');
      const name = document.getElementById('item-name').value;
      const pay = parseFloat(document.getElementById('item-value').value) || 0;
      if (pay <= 0 || name.trim() == ""){
        return;
      }
      const payment = {
          name, 
          value: pay,
          completed: true,
          type: 'payment'
        }
      this.payments = [...this.payments, payment];
      form.reset();
    }
  }
};
</script>

<style>
.ledger-item {
  display: flex;
  justify-content: space-between;
  padding: 0px;
}
#ledger-list {
  margin-top: 1rem;
  list-style-type: none;
}
.bill-value {
  color: red;
}
.payment{
  color: green;
}
</style>