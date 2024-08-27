<template>
  <table>
    <tr>
      <th>#</th>
      <th>Task</th>
      <th>Status</th>
      <th>Action</th>
    </tr>
    <tr v-for="(item, index) in items" :key="index">
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
};
</script>

<style scoped>
.item {
  background: #e6e6e6;
  padding: 5px;
  margin-top: 5px;
}
</style>
