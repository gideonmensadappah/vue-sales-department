 <template>
  <div class="table" v-on:keyup.13="updateCustomer">
    <div v-if="isEditing">
      <input type="text" v-model="customer.fullName" />
    </div>
    <div v-else>
      <div>{{ customer.fullName }}</div>
    </div>
    <div v-if="isEditing">
      <input type="text" v-model="customer.phone" />
    </div>
    <div v-else>
      <div>{{ customer.phone }}</div>
    </div>
    <div v-if="isEditing">
      <input type="text" v-model="customer.city" />
    </div>

    <div v-else>
      <div>{{ customer.city }}</div>
    </div>
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
  data() {
    return {
      isEditing: false,
    };
  },
  methods: {
    // dispatch edit action
    editCustomer() {
      if (this.isEditing) {
        console.log("emiting");
        this.$emit("edit-customer", this.customer);
        this.isEditing = false;
      } else {
        this.isEditing = true;
      }
    },

    // dispatch delete action
    async deleteCustomer() {
      try {
        const response = await fetch(
          `http://localhost:3000/${this.customer._id}`,
          {
            method: "DELETE",
          }
        );
        this.$emit("deleted-customer", this.customer._id);
        const result = await response.json();

        alert(result.msg);
      } catch (err) {
        console.log(err);
      }
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

