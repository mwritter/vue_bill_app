<template>
  <main>
    <div class="container">
      <div id="heading">
        <h1 class="text">Bill Checklist</h1>
      </div>
      <ul id="bill-list">
        <li class="bill-list-item" v-for="(bill) in bills" :key="bill.name">
          <div>
            <input @click="toggleBill(bill)" :id="bill.name" type="checkbox" />
            <label class="text" for="price">{{bill.name}}</label>
          </div>
          <span id="price" class="text" name="price">${{bill.value}}</span>
        </li>
      </ul>
    </div>
  </main>
</template>

<script>
export default {
  name: "BillChecklist",
  props: {
    bills: {
      type: Array
    }
  },
  mounted() {
    for (const bill of this.bills) {
      if (bill.complete) {
        document.getElementById(bill.name).checked = true;
      }
    }
  },
  methods: {
    toggleBill(bill) {
      this.$emit("toggleBill", bill);
    }
  }
};
</script>

<style>
#bill-list {
  padding: 0px;
}
.bill-list-item {
  display: flex;
  justify-content: space-between;
}
</style>