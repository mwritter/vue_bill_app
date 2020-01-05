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
      <div id="new-misc">
        <input type="text">
        <input type="number">
        <button @click="this.addMisc()">Submit</button>
      </div>
      <div class="text misc-list-item">
        <span>Total Spent</span>
        <span>${{this.getTotalSpent}}</span>
      </div>
      <div class="text misc-list-item">
        <span>Remaining</span>
        <span></span>
      </div>
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
      adding: true
    }
  },
  computed: {
    getTotalSpent() {
      return this.miscs.reduce((total, item) => {
        return total + item.value;
      }, 0);
    }
  },
  methods: {
    addMisc(misc){
      this.$emit('addMisc', misc)
    }
  }
};
</script>

<style>
#misc-list {
  list-style-type: none;
}
.misc-list-item {
  display: flex;
  justify-content: space-between;
}
.misc-value {
  color: red;
}
</style>