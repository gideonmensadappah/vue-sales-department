 <template>
  <div class="table">
    <div>{{ customer.fullName }}</div>
    <div>{{ customer.phone }}</div>
    <div>{{ customer.city }}</div>
    <div>
      <button @click="editCustomer">Edit</button> |
      <button @click="deleteCustomer">Delete</button>
    </div>
  </div>
</template>

 <script>
export default {
  name: "CustomersList",
  props: ["customer"],
  methods: {
    // dispatch edit action
    editCustomer() {
      console.log({ customer: this.customer, msg: "editCustomer" });
    },
    // dispatch delete action
    deleteCustomer() {
      console.log({ customer: this.customer, msg: "deleteCustomer" });
    },
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

