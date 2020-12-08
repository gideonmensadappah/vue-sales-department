<template>
  <div id="app">
    <CustomersTable v-bind:customers="customers" />
    <div class="add-customer">
      <input v-if="isNewCustomer" placeholder="fullName" />
      <input placeholder="phone" v-if="isNewCustomer" />
      <input placeholder="city" v-if="isNewCustomer" />
      <button @click="newCustomer">Add Customer</button>
    </div>
  </div>
</template>

<script>
/**
 
 * dispatch add customer
 */

import CustomersTable from "./components/CustomersTable";

export default {
  name: "App",
  data() {
    return {
      isNewCustomer: false,
      customers: [
        {
          id: 1,
          fullName: "gideon mensa",
          phone: "05430434943",
          city: "Tel-aviv",
        },
        { id: 2, fullName: "dan mensa", phone: "05423454943", city: "ashdod" },
        { id: 3, fullName: "yosef haom", phone: "0903212321", city: "Tel-hai" },
        { id: 4, fullName: "dan sad", phone: "05425764943", city: "ashdod" },
      ],
    };
  },
  components: {
    CustomersTable,
  },
  methods: {
    newCustomer() {
      if (this.isNewCustomer) {
        alert("adding new Customer!");
        this.isNewCustomer = !this.isNewCustomer;
      } else {
        this.isNewCustomer = !this.isNewCustomer;
      }
    },
  },
};
</script>

<style>
.add-customer {
  padding: 5px;
}
input {
  margin: 4px;
}
</style>
