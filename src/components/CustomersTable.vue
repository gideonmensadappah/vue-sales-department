<template>
  <div>
    <div class="table">
      <div>Full Name</div>
      <div>Phone</div>
      <div>City</div>
      <div>Actions</div>
    </div>
    <div v-for="customer in customers" :key="customer.id">
      <Customer v-bind:customer="customer" />
    </div>
  </div>
</template>
<script>
import Customer from "./Customer";

export default {
  name: "CustomersTable",
  props: ["customers"],
  components: {
    Customer,
  },
};
</script>

<style scoped>
.table {
  display: grid;
  grid-template-columns: repeat(auto-fill, 13%);
  padding: 10px;
  border-bottom: 1px black solid;
}
</style>