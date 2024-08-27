<template>
  <td>{{ item.id }}</td>
  <td>
    <span :class="[item.completed ? 'completed' : '', 'itemText']">{{
      item.name
    }}</span>
  </td>
  <td>{{ item.completed ? "Completed" : "" }}</td>
  <td>
    <button
      v-if="!item.completed"
      @click="
        item.completed = true;
        updateCheck(item.id);
      "
      class="btn btn-success btn-sm me-1"
    >
      Complete
    </button>
    <button @click="removeItem()" class="btn-sm btn btn-danger">
      <font-awesome-icon icon="trash" />
    </button>
  </td>
</template>

<script>
export default {
  props: ["item"],
  methods: {
    updateCheck(id) {
      axios
        .put("api/item/" + id, {
          item: this.item,
        })
        .then((response) => {
          if (response == 200) {
            this.$emit("itemChanged");
          }
        })
        .catch((error) => {
          console.log(error);
        });
    },
    removeItem() {
      if (confirm("Are you sure you want to delete ?"))
        axios
          .delete("api/item/" + this.item.id)
          .then((response) => {
            if (response.status == 200) {
              this.$emit("itemChanged");
            }
          })
          .catch((error) => {
            console.log(error);
          });
    },
  },

  mounted() {},
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  color: #999;
}

.itemText {
  width: 100%;
  margin-left: 20px;
}

.item {
  display: flex;
  justify-content: center;
  align-items: center;
}

.trashcan {
  background: #e6e6e6;
  border: none;
  color: #ff0000;
  outline: none;
  cursor: pointer;
}
</style>
