<template>
  <div id="app">
    <h1>Product Management</h1>
    <AddProduct @product-added="addProduct" />
    <ProductList :products="products" @delete-product="deleteProduct" @edit-product="editProduct" />
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
