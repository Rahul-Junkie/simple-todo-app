<template>
<div class="container my-5 card">
    <div class="heading">
      <h2 id="title">PHP - Simple To Do List App</h2>
      <addItemForm @reloadlist="getList()" />
    </div>
    <listView :items="items" @reloadlist="getList()" />
  </div>
</template>

<script>
import addItemForm from "./addItemForm.vue";
import listView from "./listView.vue";
export default {
  data() {
    return {
      items: [],
    };
  },
  components: {
    addItemForm,
    listView,
  },
  methods: {
    getList() {
      axios
        .get("api/items")
        .then((response) => {
          this.items = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  mounted() {
    this.getList();
  },
};
</script>

<style scoped>
.todoListContainer {
  margin: auto;
}

.heading {
  padding: 10px;
}

#title {
  text-align: center;
  color: rgb(17, 120, 179);
}
</style>
