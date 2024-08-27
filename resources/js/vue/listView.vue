<template>
 <button @click="toggleFilter" class="btn btn-success btn-sm col-sm-2">
      {{ showCompleted ? 'Show Non completed' : 'Show All' }}
    </button>
  <table>
    <tr>
      <th>#</th>
      <th>Task</th>
      <th>Status</th>
      <th>Action</th>
    </tr>
    <tr v-for="(item, index) in filteredItems" :key="index">
      <listItem :item="item" class="item" @itemChanged="$emit('reloadlist')" />
    </tr>
  </table>
</template>

<script>
import listItem from "./listItem.vue";
export default {
  props: ["items"],
  components: {
    listItem,
  },
  data() {
    return {
      showCompleted: false, // Default to showing incomplete tasks
    };
  },
  computed: {
    filteredItems() {
      return this.showCompleted ? this.items : this.items.filter(item => !item.completed);
    },
  },
  methods: {
    toggleFilter() {
      this.showCompleted = !this.showCompleted;
    },
  },
};
</script>

<style scoped>
.item {
  background: #e6e6e6;
  padding: 5px;
  margin-top: 5px;
}
</style>
