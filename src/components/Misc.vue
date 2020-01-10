<template>
  <main>
    <div class="container">
      <div>
        <h1 id="heading" class="text">Miscellaneous</h1>
        <ul id="misc-list">
          <li class="text misc-list-item" v-for="misc in miscs" :key="misc.id">
            <div class="misc-name">{{misc.name}}</div>
            <span
              @click="deleteMisc(misc)"
              title="Remove Misc Item"
              class="small-btn small-danger-btn action-btn"
            ></span>
            <span class="misc-value">-${{misc.value}}</span>
          </li>
        </ul>

        <div id="misc-info">
          <div class="text misc-list-item">
            <div>Total Spent</div>
            <span>Pizza</span>
            <span>${{this.getTotalSpent}}</span>
          </div>
          <div class="text misc-list-item">
            <div>Remaining</div>
            <span>Pizza</span>
            <span>${{this.getRemaining}}</span>
          </div>
          <form v-if="this.adding" id="new-misc-form" @submit.prevent>
            <div id="form-inputs">
              <input
                class="text"
                placeholder="Description"
                name="misc-item-name"
                id="misc-item-name"
                type="text"
              />
              <input
                class="text"
                placeholder="Price"
                step="0.01"
                min="1"
                name="misc-item-value"
                id="misc-item-value"
                type="number"
              />
            </div>

            <div class="action-section">
              <button
                class="action-btn small-btn small-success-btn"
                title="Submit Misc"
                @click="addMisc()"
              ></button>
              <button
                class="action-btn small-btn small-danger-btn"
                title="Cancel"
                @click="cancelMisc()"
              ></button>
            </div>
          </form>
        </div>
      </div>

      <div id="add-section">
        <div @click="adding = true" title="Add Misc Item" class="action-btn add-btn" id="add-misc">+</div>
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
        return total + parseFloat(item.value);
      }, 0);
    },
    getRemaining() {
      return this.currentTotal - this.accountLimit;
    }
  },
  methods: {
    addMisc() {
      const input_value = document.getElementById("misc-item-value");
      const input_name = document.getElementById("misc-item-name");
      const form = document.getElementById("new-misc-form");

      let value = input_value.value || 0;

      if (input_value <= 0 || input_name.value.trim() == "") {
        return;
      }
      const misc = {
        id: this.miscs.length + 1,
        complete: true,
        value: value,
        name: input_name.value
      };
      this.adding = !this.adding;
      form.reset();
      this.$emit("addMisc", misc);
    },
    deleteMisc(misc) {
      this.$emit("deleteMisc", misc);
    },
    cancelMisc() {
      const form = document.getElementById("new-misc-form");
      form.reset();
      this.adding = !this.adding;
    }
  }
};
</script>

<style>
#misc-info {
  margin-top: 2rem;
}

.misc-list-item {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  padding-left: 1rem;
  padding-right: 1rem;
  border: 1px solid white;
}
.small-btn {
  align-self: center;
}

.misc-list-item:hover .small-danger-btn {
  visibility: visible;
}
.misc-list-item .small-danger-btn {
  visibility: hidden;
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

#misc-delete-btn {
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  height: 25px;
  width: 25px;
}
#new-misc-form {
  margin-top: 1rem;
}
#form-inputs {
  display: grid;
  grid-template-columns: auto auto;
  grid-column-gap: 1rem;
}
</style>