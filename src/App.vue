<template>
  <div id="app">
    <div class="container">
      <div class="product-list">
        <h2 class="title">Product List</h2>
        <table>
          <thead>
            <tr>
              <th>Product Name</th>
              <th>Price</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="product in products" :key="product.id">
              <td>{{ product.name }}</td>
              <td>₱{{ product.price }}</td>
              <td>
                <button class="action-btn" @click="addToCart(product)">Add to Cart</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="cart">
        <h2 class="title">Cart</h2>
        <div v-if="cartItems.length === 0">
          <p>Cart is empty</p>
        </div>
        <div v-else>
          <table>
            <thead>
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
                <td>₱{{ item.price }}</td>
                <td>
                  <button class="quantity-btn" @click="decrement(item)">-</button>
                  {{ item.quantity }}
                  <button class="quantity-btn" @click="increment(item)">+</button>
                </td>
                <td>₱{{ item.price * item.quantity }}</td>
                <td>
                  <button class="action-btn" @click="removeFromCart(item)">Remove</button>
                </td>
              </tr>
            </tbody>
          </table>
          <p class="total">Total Price: ₱{{ total }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
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
      ],
      cartItems: [],
      containerHeight: null // Store container height
    };
  },
  computed: {
    total() {
      return this.cartItems.reduce((total, item) => total + item.price * item.quantity, 0);
    }
  },
  methods: {
    addToCart(product) {
      const existingItem = this.cartItems.find(item => item.id === product.id);
      if (existingItem) {
        existingItem.quantity++;
      } else {
        this.cartItems.push({ ...product, quantity: 1 });
      }
      alert('Product successfully added to cart!');
    },
    increment(item) {
      item.quantity++;
      this.updateContainerHeight();
    },
    decrement(item) {
      if (item.quantity > 1) {
        item.quantity--;
        this.updateContainerHeight();
      }
    },
    removeFromCart(item) {
      this.cartItems = this.cartItems.filter(cartItem => cartItem.id !== item.id);
      alert('Product successfully removed from cart!');
      this.updateContainerHeight();
    },
    updateContainerHeight() {
      // Update container height after DOM update
      this.$nextTick(() => {
        const container = document.querySelector('.container');
        this.containerHeight = container.offsetHeight + 'px';
      });
    }
  }
};
</script>

<style scoped>
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: orange;
}

.container {
  display: flex;
  min-height: 100%; /* Ensure container takes up full height */
}

.product-list, .cart {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 10px;
  background-color: #fff;
}

.product-list {
  flex: 1;
}

.cart {
  margin-left: 20px;
  min-width: 300px;
}

.title {
  margin: 0 0 10px;
  text-align: center;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}

.action-btn {
  background-color: #888;
  color: white;
  padding: 6px 10px;
  border: none;
  cursor: pointer;
  border-radius: 3px;
}

.quantity-btn {
  background-color: #888;
  color: white;
  padding: 6px;
  border: none;
  cursor: pointer;
  border-radius: 3px;
}

.quantity-btn:hover {
  background-color: #666;
}
</style>
