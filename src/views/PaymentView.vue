<template>
  <div class="background">
    <div class="container">
      <!-- Logo and Title -->
      <div class="row logo">
        <img src="../assets/logo_orange.png" alt="Logo">
      </div>
      <div class="row title">
        <h1>Payment</h1>
      </div>

      <!-- Client Name and Purchase Type -->
      <div class="row">
        <input type="text" id="clientName" class="textbox-client" placeholder="Name of Client" />
      </div>
      <div class="row">
        <select id="purchaseType" class="textboxes">
          <option>Walk In</option>
          <option>Online</option>
        </select>
      </div>

      <!-- Product List Container -->
      <div class="productcontainer">
        <div class="product-line" v-for="(product, index) in products" :key="index">
          <div class="product-col col1">
            <div class="product-name">{{ product.name }}</div>
            <div class="product-size">{{ product.size }} mm</div>
          </div>
          <div class="product-col col2">{{ product.price }}</div>
          <div class="product-col col3">
            <div class="quantity-container">
              <input type="text" class="quantity-input" v-model="product.quantity" readonly />
            </div>
          </div>
          <div class="product-col col4">{{ (product.quantity * product.price).toFixed(2) }}</div>
        </div>
      </div>

      <!-- Overall Totals -->
      <div class="producttotalcontainer">
        <div class="product-line">
          <div class="product-col col1">
            <div class="item-count">Item: {{ totalItems }}</div>
            <div class="quantity-label">Qty: {{ totalQuantity }}</div>
          </div>
          <div class="product-col col2">
            <label class="total-label">Total</label>
          </div>
          <div class="product-col col3">{{ totalPrice.toFixed(2) }}</div>
        </div>
      </div>

      <!-- Payment Method Section -->
      <div class="row payment-method">
        <label for="paymentMethod">Payment Method</label>
        <div class="paymentinputcontainer">
          <select id="paymentMethod" class="textboxes" v-model="selectedPaymentMethod">
            <option>Gcash</option>
            <option>COD</option>
          </select>
          <input type="text" id="clientPayment" class="textboxpayment" v-model="amountPaid" placeholder="Enter amount" />
        </div>
      </div>

      <!-- Change Display -->
      <div class="changecontainer">
        <label for="change">Change</label>
        <span class="change-amount">{{ changeAmount }}</span>
      </div>

      <div class="row staff-section">
        <label for="staffName">Staff</label>
        <input type="text" id="staffName" class="textbox-staff" v-model="staffName" placeholder="Enter Staff Name" />
      </div>

      <!-- Submit Button -->
      <div class="submitcontainer">
        <button class="submit-button" @click="submitOrder">SUBMIT</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [
        { name: 'Product 1', price: 100, quantity: 1, size: 50 },
        { name: 'Product 2', price: 150, quantity: 5, size: 100 },
      ],
      selectedPaymentMethod: 'Gcash', // Default selection for payment method
      amountPaid: 0, // Amount paid by the client
      staffName: '' // New property for staff name
    };
  },
  computed: {
    totalPrice() {
      return this.products.reduce((total, product) => total + (product.price * product.quantity), 0);
    },
    totalItems() {
      return this.products.length; // Count the number of unique products
    },
    totalQuantity() {
      return this.products.reduce((total, product) => total + product.quantity, 0);
    },
    changeAmount() {
      const change = (this.amountPaid - this.totalPrice).toFixed(2);
      return change >= 0 ? change : "0.00"; // Display 0.00 if negative
    },
  },
  methods: {
    submitOrder() {
      // Logic to submit the order
      this.$router.push('/receipt');
    },
  }
};
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
}

.background {
  background-color: rgb(233, 161, 29);
  height: 100vh;
  width: 100vw;
  display: flex;
  align-items: center;
  justify-content: center;
}

.container {
  width: calc(100% - 20px); /* Adjusted to avoid overflow due to padding */
  height: calc(100% - 20px); /* Adjusted to avoid overflow due to padding */
  background-color: white;
  border: 2px solid rgb(233, 161, 29);
  border-radius: 20px;
  box-sizing: border-box;
  padding: 15px 20px; /* Reduced padding */
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 15px;
}

.row {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 5px;
}

.logo img {
  width: 180px;
  display: block;
  margin: auto;
  margin-top: -40px;
}

.title h1 {
  text-align: center;
  width: 100%;
  margin: 0;
  font-size: 22px;
  margin-top: -20px;
}

.textboxes {
  width: 100%;
  padding: 5px;
  border: 1px solid rgb(233, 161, 29);
  border-radius: 5px;
  font-size: 16px;
}

.textbox-client {
  width: 96%;
  padding: 5px;
  border: 1px solid rgb(233, 161, 29);
  border-radius: 5px;
  font-size: 16px;
}

.textboxpayment {
  flex: 0; /* Allow the textbox to fill available space */
  padding: 5px;
  border: 1px solid rgb(233, 161, 29);
  border-radius: 5px;
  font-size: 16px;
  margin-left: 40px;
}
.textbox-staff {
  flex: 0; /* Allow the textbox to fill available space */
  padding: 5px;
  border: 1px solid rgb(233, 161, 29);
  border-radius: 5px;
  font-size: 16px;
  margin-left: 40px;
}


.productcontainer {
  width: 100%;
  border: 1px solid rgb(233, 161, 29);
  border-radius: 10px;
  margin-top: 10px;
  font-weight: bold;
  color: #474343;
}

.producttotalcontainer {
  width: 100%;
  border: 1px solid rgb(233, 161, 29);
  border-radius: 10px;
  margin-top: 0;
  font-weight: bold;
  color: #474343;
}

.product-line {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1fr 0.5fr;
  align-items: center;
  padding: 5px;
}

.product-col {
  padding: 5px;
}

.quantity-input {
  width: 50px;
  text-align: left;
  border: none; /* Removes the border */
  padding: 7px;
  font-size: 14px;
}

.staff-section {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-top: 3px;
}

.payment-method {
  display: flex;
  align-items: start; /* Align items vertically center */
  gap: 10px; /* Space between select and input */
}

.paymentinputcontainer {
  display: flex;
  align-items: center; /* Center align input and select */
}

.textbox {
  flex: 1; /* Allow textbox to fill available space */
  margin-right: 10px; /* Add some space between select and input */
}

#clientPayment {
  width: 150px; /* Set a fixed width for the amount input */
}

.changecontainer {
  display: flex; /* Use flexbox for layout */
  align-items: center; /* Vertically center the items */
  border: 1px solid rgb(233, 161, 29); /* Add border */
  border-radius: 10px; /* Optional: rounded corners */
  padding: 7px; /* Optional: padding for aesthetics */
  width: 92%;
}

.change-container label {
  flex: 1; /* Allow label to take available space */
  margin-right: 10px; /* Space between label and amount */
  font-weight: bold; /* Make label bold for emphasis */
}

.change-amount {
  font-weight: bold; /* Make change amount bold */
  margin-left: auto; /* Align to the right of the container */
}

.submitcontainer {
  display: flex;
  justify-content: flex-end;
  width: 100%;
  margin-top: 13px;
}

.submit-button {
  background-color: #ff914d;
  color: white;
  border: none;
  border-radius: 5px;
  padding: 5px 30px;
  font-size: 14px;
  cursor: pointer;
}
</style>
