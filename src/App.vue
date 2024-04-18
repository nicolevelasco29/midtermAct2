<template>
  <div id="app" class="container">
    <h1 class="title">Product Management</h1>
    <div class="columns">
      <div class="column">
        <AddProduct @product-added="addProduct" />
      </div>
      <div class="column">
        <ProductList :products="products" @delete-product="deleteProduct" @edit-product="editProduct" />
      </div>
    </div>
  </div>
</template>

<script>
import AddProduct from './components/AddProduct.vue';
import ProductList from './components/ProductList.vue';

export default {
  components: {
    AddProduct,
    ProductList
  },
  data() {
    return {
      products: [],
      editingProduct: null
    };
  },
  methods: {
    addProduct(newProduct) {
      this.products.push(newProduct);
    },
    deleteProduct(productId) {
      this.products = this.products.filter(product => product.id !== productId);
    },
    editProduct(product) {
      this.editingProduct = product;
    },
    updateProduct(updatedProduct) {
      const index = this.products.findIndex(product => product.id === updatedProduct.id);
      if (index !== -1) {
        this.products.splice(index, 1, updatedProduct);
      }
      this.editingProduct = null;
    }
  }
};
</script>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.title {
  text-align: center;
  margin-bottom: 20px;
}

.columns {
  display: flex;
  justify-content: space-between;
}
</style>