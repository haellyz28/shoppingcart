<template>
    <div class="product-item">
      <h2 class="title">Product List</h2>
      <table>
        <thead>
          <tr>
            <th colspan="3">Product List</th>
          </tr>
          <tr>
            <th>Product Name</th>
            <th>Price</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="product in products" :key="product.id">
            <td>{{ product.name }}</td>
            <td>${{ product.price }}</td>
            <td>
              <button @click="addToCart(product)">Add to Cart</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ProductList',
    data() {
      return {
        products: [
        { id: 1, name: 'Chicago Short', price: 65 },
        { id: 2, name: 'Vans Skate Style Shoes', price: 1700 },
        { id: 3, name: 'NY Yankees New York Green baseball caps', price: 250 },
        { id: 4, name: 'Essentials Pocket Tees Corduroy', price: 280 },
        { id: 5, name: 'Quarterzip Polo Sweater', price: 280 },
        { id: 6, name: 'Lansite Trendy High Waist Pants', price: 215 },
        { id: 7, name: 'Mens Jeans Baggy Pants', price: 200 },
        { id: 8, name: 'Crocs Mens Clogs', price: 300 },
        { id: 9, name: 'Trend Corduroy Shorts', price: 85 },
        { id: 10, name: 'Snapback Cap Daffy Duck', price: 160 }
        ]
      };
    },
    methods: {
      addToCart(product) {
        this.$emit('add-to-cart', product);
        alert('Product successfully added to cart!');
      }
    }
  };
  </script>
  
  <style scoped>
  .product-item {
    border: 1px solid #ccc;
    padding: 10px;
    margin-bottom: 10px;
    display: flex;
    flex-direction: column;
  }
