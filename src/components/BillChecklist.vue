<template>
  <main>
    <div class="container">
      <div>
        <h1 id="heading" class="text">Bill Checklist</h1>
        <ul id="bill-list">
          <li class="bill-list-item" v-for="(bill) in bills" :key="bill.name">
              <!-- <input class="checkbox" @click="toggleBill(bill)" :id="bill.name" type="checkbox" /> -->
            <span class="text bill-name">{{bill.name}}</span>
            <span @click="toggleBill(bill)" :class="{'small-success-btn': bill.complete }" class="bill-checkbox action-btn small-btn"></span>
            <span class="text bill-price" name="price">${{bill.value}}</span>
          </li>
        </ul>
      </div>

      <div id="add-section">
        <div @click="adding = true" class="action-btn add-btn" id="add-bill">+</div>
      </div>
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
.bill-price{
  grid-area: price;
}
.bill-name{
  grid-area: name;
  justify-self: start;
}
.bill-checkbox{
  grid-area: checkbox;
}
.bill-list-item {
  display: grid;
  grid-gap: 1rem;
  grid-template-columns: auto 2fr auto;
  grid-template-areas: "checkbox name price";
}
</style>