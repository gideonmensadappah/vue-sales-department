<template>
  <div id="app">
    <CustomersTable
      @edit-customer="editCustomer"
      @deleted-customer="updatedCustomersList"
      v-bind:customers="customers"
    />
    <div class="add-customer">
      <input v-if="isNewCustomer" v-model="fullName" placeholder="fullName" />
      <input placeholder="phone" v-model="phone" v-if="isNewCustomer" />
      <input placeholder="city" v-model="city" v-if="isNewCustomer" />
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
      fullName: "",
      phone: "",
      city: "",
      isNewCustomer: false,
      customers: [],
    };
  },
  components: {
    CustomersTable,
  },
  async beforeUpdated() {
    this.getUsers();
  },
  methods: {
    async editCustomer(value) {
      const newCustomer = {
        _id: value._id,
        fullName: value.fullName,
        phone: value.phone,
        city: value.city,
      };

      console.log(newCustomer);
      const putMethod = {
        method: "PUT",
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
        body: JSON.stringify(newCustomer),
      };

      await fetch(`http://localhost:3000/`, putMethod);
    },
    updatedCustomersList(customerId) {
      this.customers = this.customers.filter(
        (customer) => customer._id != customerId
      );
    },

    async newCustomer() {
      if (this.isNewCustomer) {
        const isValid = this.fullName && this.phone && this.city;
        if (isValid) {
          await fetch("http://localhost:3000/", {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify({
              fullName: this.fullName,
              phone: this.phone,
              city: this.city,
            }),
          });

          this.fullName = "";
          this.phone = "";
          this.city = "";

          this.isNewCustomer = !this.isNewCustomer;
          this.getUsers();
        }
      } else {
        this.isNewCustomer = !this.isNewCustomer;
      }
    },
    async getUsers() {
      const customersList = await fetch("http://localhost:3000/");
      const customers = await customersList.json();
      this.customers = customers;
    },
  },
  mounted() {
    this.getUsers();
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
