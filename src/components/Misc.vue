<template>
  <main>
    <div class="container">
      <div id="heading">
        <h1 class="text">Miscellaneous</h1>
      </div>
      <ul id="misc-list">
        <li class="text misc-list-item" v-for="misc in miscs" :key="misc.id">
          <span>{{misc.name}}</span>
          <span class="misc-value">-${{misc.value}}</span>
        </li>
      </ul>
      <div v-if="adding" id="new-misc">
        <input class="text" name="misc-item-name" id="misc-item-name" type="text" />
        <input class="text" name="misc-item-value" id="misc-item-value" type="number" />
        <button @click="addMisc()">Submit</button>
        <button @click="cancelMisc()">Cancel</button>
      </div>
      <div class="text misc-list-item">
        <span>Total Spent</span>
        <span>${{this.getTotalSpent}}</span>
      </div>
      <div class="text misc-list-item">
        <span>Remaining</span>
        <span></span>
      </div>
      <div @click="adding = true" class="add-btn" id="add-misc">+</div>
    </div>
  </main>
</template>

<script>
export default {
  name: "Misc",
  props: {
    miscs: {
      type: Array
    }
  },
  data: () => {
    return {
      adding: false
    };
  },
  computed: {
    getTotalSpent() {
      return this.miscs.reduce((total, item) => {
        return total + item.value;
      }, 0);
    }
  },
  methods: {
    addMisc() {
      const value = parseFloat(
        document.getElementById("misc-item-value").value || 0
      );
      const name = document.getElementById("misc-item-name").value;

      if (value == 0 || name.trim() == "") {
        return;
      }

      const misc = {
        id: this.miscs.length + 1,
        complete: true,
        value,
        name
      };
      this.adding = !this.adding;
      this.$emit("addMisc", misc);
    },
    cancelMisc() {
      this.adding = !this.adding;
    }
  }
};
</script>

<style>
#misc-list {
  list-style-type: none;
  margin-bottom: 2rem;
}
.misc-list-item {
  display: flex;
  justify-content: space-between;
}
.misc-value {
  color: red;
}
</style>