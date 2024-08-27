<template>
  <!-- To-Do Form -->
  <div class="row">
    <div class="col-md-9">
      <div class="mb-3">
        <input
          type="text"
          class="form-control"
          v-model="item.name"
          id="taskInput"
          placeholder="Enter a new task"
          required
        />
      </div>
    </div>
    <div class="col-md-3">
      <button type="button" @click="addItem()" class="btn btn-primary">
        Add Task
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      item: {
        name: "",
      },
    };
  },
  methods: {
    addItem() {
      
      axios
        .post("api/item/store", {
          item: this.item,
        })
        .then((response) => {
          if (response.status == 201) {
            this.item.name = "";
            this.$emit("reloadlist");
          }
        })
        .catch((error) => {
          alert(error.response.data.message);
        });
    },
  },
};
</script>

<style scoped>
.addItem {
  display: flex;
  justify-content: center;
  align-items: center;
}

input {
  background: #f7f7f7;
  border: 0;
  outline: none;
  padding: 5px;
  margin-right: 10px;
}

.plus {
  font-size: 20px;
  cursor: pointer;
}

.active {
  color: #00ce25;
}

.inactive {
  color: #999;
}
</style>
