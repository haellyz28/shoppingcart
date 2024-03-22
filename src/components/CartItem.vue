<template>
    <div class="cart-item">
      <h2 class="title">Cart</h2>
      <div v-if="cartItems.length === 0">
        <p>Cart is empty</p>
      </div>
      <div v-else>
        <table>
          <thead>
            <tr>
              <th colspan="5">Cart</th>
            </tr>
            <tr>
              <th>Product Name</th>
              <th>Price</th>
              <th>Quantity</th>
              <th>Total Price</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in cartItems" :key="item.id">
              <td>{{ item.name }}</td>
              <td>${{ item.price }}</td>
              <td>
                <button @click="decrement(item)">-</button>
                {{ item.quantity }}
                <button @click="increment(item)">+</button>
              </td>
              <td>${{ item.price * item.quantity }}</td>
              <td>
                <button @click="removeFromCart(item)">Remove</button>
              </td>
            </tr>
          </tbody>
        </table>
        <p class="total">Total Price: ${{ total }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'CartItem',
    props: {
      cartItems: Array
    },
    computed: {
      total() {
        return this.cartItems.reduce((total, item) => total + item.price * item.quantity, 0);
      }
    },
    methods: {
      increment(item) {
        this.$emit('increment-quantity', item);
      },
      decrement(item) {
        this.$emit('decrement-quantity', item);
      },
      removeFromCart(item) {
        this.$emit('remove-from-cart', item);
      }
    }
  };
  </script>
  
  <style scoped>
  .cart-item {
    border: 1px solid #ccc;
    padding: 10px;
    margin-bottom: 10px;
    text-align: center; /* Center align the content */
  }
  
  </style>
