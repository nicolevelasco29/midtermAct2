<template>
  <div class="product-list">
    <h2>Product List</h2>
    <table class="table">
      <thead>
        <tr>
          <th>Product ID</th>
          <th>Product Name</th>
          <th>Description</th>
          <th>Price</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td>{{ product.id }}</td>
          <td>{{ product.name }}</td>
          <td>{{ product.description }}</td>
          <td>{{ product.price }}</td>
          <td>
            <button @click="editProduct(product)" class="button is-primary is-small">Edit</button>
            <button @click="deleteProduct(product.id)" class="button is-danger is-small">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    products: Array
  },
  methods: {
    editProduct(product) {
      this.$emit('edit-product', product);
    },
    deleteProduct(productId) {
      this.$emit('delete-product', productId);
    }
  }
};
</script>

<style scoped>
.table {
  width: 100%;
  border-collapse: collapse;
}

.table th, .table td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

.table th {
  background-color: #f2f2f2;
}

.button {
  margin-right: 5px;
}
</style>
