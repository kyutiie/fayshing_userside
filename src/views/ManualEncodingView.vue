<template>
  <div class="background">
      <div class="container">
          <div class="row logo">
              <img src="../assets/logo_orange.png" alt="Logo">
          </div>
          <div class="row title">
              <h1>Manual Encoding</h1>
          </div>
          <div class="row search-container">
              <input type="text" class="textboxes" v-model="searchQuery" placeholder="Search product Code, Nam.." @input="searchProducts">
              <svg class="search-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path fill="rgb(233, 161, 29)" d="M10.5 2C5.81 2 2 5.81 2 10.5S5.81 19 10.5 19c2.68 0 5.06-1.04 6.85-2.73l5.59 5.59c.39.39 1.02.39 1.41 0s.39-1.02 0-1.41l-5.59-5.59A8.5 8.5 0 0010.5 2zm0 15c-2.61 0-4.76-2.15-4.76-4.76S7.89 7.5 10.5 7.5s4.76 2.15 4.76 4.76-2.15 4.76-4.76 4.76z"/></svg>
          </div>
          <div class="row">
              <label>Product Code</label>
              <input type="text" class="textboxes">
          </div>
          <div class="row">
              <label>Product Name</label>
              <input type="text" class="textboxes">
          </div>
          <div class="row">
              <label>Price</label>
              <input type="text" class="textboxes">
          </div>
          <div class="row">
              <label>Colors</label>
              <select class="textboxes">
                  <option>Select Color</option>
                  <option>Red</option>
                  <option>Blue</option>
                  <option>Green</option>
                  <option>Black</option>
              </select>
          </div>
          <div class="row sizes">
      <label>Size</label>
      <div class="size-options">
        <div class="circle-option">
          <input type="radio" id="size50" name="size" value="50ml">
          <label for="size50">50ml</label>
        </div>
        <div class="circle-option">
          <input type="radio" id="size100" name="size" value="100ml">
          <label for="size100">100ml</label>
        </div>
        <div class="circle-option">
          <input type="radio" id="size150" name="size" value="150ml">
          <label for="size150">150ml</label>
        </div>
      </div>
    </div>
    <div class="row quantity">
        <label>Quantity</label>
        <div class="quantitycontainer">
    <input 
      type="number" 
      class="textbox quantity-input" 
      v-model="quantity" 
      min="1" 
      @input="validateQuantity"
    >
    <div class="arrow-container">
        <span class="arrow-up" @click="increaseQuantity"></span>
        <span class="arrow-down" @click="decreaseQuantity"></span>
    </div>
</div>
      </div>
          <div class="row">
              <label>Total Price</label>
              <input type="text" class="textboxes">
          </div>
          <div class="row submit">
              <button class="submit-button"@click="submitOrder">SUBMIT</button>
          </div>
          <div class="row center-button">
              <button class="button-group" @click="goToHome">Cancel</button>
          </div>
      </div>
  </div>
</template>

<script>
export default {
  data() {
      return {
          quantity: 1, // Initialize quantity
          searchQuery: '', // Initialize search query
      };
  },
  methods: {
      goToHome() {
          this.$router.push('/home'); // Navigate to the home route
      },
      increaseQuantity() {
          this.quantity++; // Increment quantity
      },
      decreaseQuantity() {
          if (this.quantity > 1) {
              this.quantity--; // Decrement quantity if greater than 1
          }
      },
      searchProducts() {
          // Implement your search logic here
          console.log(`Searching for: ${this.searchQuery}`);
          // You can filter products or call an API here
      },
      submitOrder() {
            // Navigate to the payment page
            this.$router.push('/payment');
        },
  },
};
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  overflow: hidden;
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
  width: calc(100% - 20px); /* Adjusted width calculation */
  max-height: 100vh; /* Set maximum height for scrollability */
  background-color: rgb(253, 248, 248);
  border: 2px solid rgb(233, 161, 29); /* Orange border */
  border-radius: 20px;
  box-sizing: border-box;
  padding:30px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 8px; /* Reduced gap for closer spacing between rows */
  overflow-y: auto; /* Enable vertical scrolling */
}


.row {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 4px; /* Increased gap for more spacing within rows */
}

.logo img {
  width: 180px;
  display: block;
  margin: auto;
  margin-top: 20px;
}

.title h1 {
  text-align: center;
  width: 100%;
  margin: 0;
  font-size: 22px;
  margin-top: -20px;
}

label {
  font-weight: 900;
}

.textboxes {
  width: 98%;
  padding: 4px; /* Reduced padding for smaller height */
  border: 1px solid rgb(233, 161, 29); /* Orange border */
  border-radius: 5px;
  font-size: 15px;
}

.search-container {
  position: relative; /* Position relative to place the icon */
  width: 100%;
}

.search-icon {
  position: absolute;
  right: 10px; /* Adjust based on your preference */
  top: 50%;
  transform: translateY(-50%);
  width: 20px;
  height: 20px;
  cursor: pointer;
  font-size: 16px;
}

.sizes {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.size-options {
  display: flex;
  gap: 25px;
  margin: 0 auto; /* Centers the .sizes container itself */
}

.circle-option {
  display: flex;
  align-items: center;
  gap: 5px;
}

.circle-option input[type="radio"] {
  appearance: none;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background-color: rgb(255, 255, 255); /* Set the default background to white */
  border: 2px solid rgb(233, 161, 29); /* Orange border for unselected */
  margin: 0;
  cursor: pointer;
  position: relative; /* Position for the inner circle */
}

.circle-option input[type="radio"]:checked {
  background-color: rgb(233, 161, 29); /* Orange background when checked */
  border: 2px solid rgb(233, 161, 29); /* Keep the border color the same when checked */
}

.circle-option input[type="radio"]:checked::after {
  content: '';
  position: absolute;
  top: 4px; /* Adjust to center the inner circle */
  left: 4px; /* Adjust to center the inner circle */
  width: 12px; /* Inner circle size */
  height: 12px; /* Inner circle size */
  border-radius: 50%; /* Make it circular */
  background-color: rgb(233, 161, 29); /* White inner circle */
}

.quantitycontainer {
  display: flex;
  align-items: center;
  width: 100%;
  position: relative;
  border: 1px solid rgb(233, 161, 29);
 border-radius: 4px;
 padding:2px;
}

.quantity-input {
  width: 100%;
  text-align: left;
  border-radius: 5px;
  padding-right: 30px;
}

.arrow-container {
  position: absolute;
  right: 5px;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.arrow-up, .arrow-down {
  width: 0;
  height: 0;
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  cursor: pointer;
}

.arrow-up {
  border-bottom: 10px solid rgb(233, 161, 29);
  margin-bottom: 2px;
}

.arrow-down {
  border-top: 10px solid rgb(233, 161, 29);
  margin-bottom: 2px;
}

.submit {
  display: flex;
  justify-content: center;
  width: 100%;
}

.submit-button {
  padding: 10px 20px;
  background-color: rgb(233, 161, 29);
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-weight: bold;
}

.center-button {
  display: flex;
  justify-content: center;
  width: 100%;
}

.button-group {
  background-color: transparent;
  border: 2px solid orange;
  border-radius: 30px;
  padding: 10px; /* Adjust padding as needed */
  cursor: pointer;
  font-size: 16px;
  color: gray;
  font-weight: bold;
  text-align: center;
  height: 40px;
}
</style>
