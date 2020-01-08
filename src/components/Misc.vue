<template>
  <main>
    <div class="container">
      <div>
        <h1 id="heading" class="text">Miscellaneous</h1>
        <ul id="misc-list">
          <li class="text misc-list-item" v-for="misc in miscs" :key="misc.id">
            <div class="misc-name">{{misc.name}}</div>
            <div @click="deleteMisc(misc)" title="Remove Misc Item" class="delete-btn"></div>
            <span class="misc-value">-${{misc.value}}</span>
          </li>
        </ul>

        <div id="misc-info">
          <div>
            <div class="text misc-list-item">
              <span>Total Spent</span>
              <span>${{this.getTotalSpent}}</span>
            </div>
            <div class="text misc-list-item">
              <span>Remaining</span>
              <span>${{this.getRemaining}}</span>
            </div>
            <div v-if="adding" id="new-misc">
              <input class="text" name="misc-item-name" id="misc-item-name" type="text" />
              <input class="text" name="misc-item-value" id="misc-item-value" type="number" />
              <button @click="addMisc()">Submit</button>
              <button @click="cancelMisc()">Cancel</button>
            </div>
          </div>
        </div>
      </div>

      <div id="add-section">
        <div @click="adding = true" title="Add Misc Item" class="action-btn" id="add-misc">+</div>
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
    },
    currentTotal: {
      type: Number
    }
  },
  data: () => {
    return {
      adding: false,
      accountLimit: 1000
    };
  },
  computed: {
    getTotalSpent() {
      return this.miscs.reduce((total, item) => {
        return total + item.value;
      }, 0);
    },
    getRemaining() {
      return this.currentTotal - this.accountLimit;
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
    deleteMisc(misc) {
      this.$emit("deleteMisc", misc);
    },
    cancelMisc() {
      this.adding = !this.adding;
    }
  }
};
</script>

<style>
#misc-info {
  margin-top: 2rem;
}
#misc-list {
  display: flex;
  flex-direction: column;
  justify-content: start;
  list-style-type: none;
}
.misc-list-item {
  display: flex;
  justify-content: space-between;
  padding-left: 1rem;
  padding-right: 1rem;
  border: 1px solid white;
}

.delete-btn {
  visibility: hidden;
  align-self: center;
  margin-right: 0.3rem;
  border: 1px solid black;
  border-radius: 50%;
  background-color: rgba(216, 122, 122, 0.589);
  width: 0.5em;
  height: 0.5em;
  cursor: pointer;
}
.misc-list-item:hover .delete-btn {
  visibility: visible;
}
.misc-list-item:hover {
  border: 1px solid rgba(216, 122, 122, 0.315);
}
#misc-info .misc-list-item:hover {
  border: 1px solid white;
}

.misc-value {
  color: red;
}
.misc-name {
  display: grid;
  grid-template-columns: auto auto;
  align-items: center;
}
#misc-delete-btn {
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  height: 25px;
  width: 25px;
}
</style>