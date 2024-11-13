<template>
  <div class="background">
    <div class="container">
      <div class="row logo">
        <img src="../assets/logo_orange.png" alt="Logo">
      </div>
      <div class="row title">
        <h1>Scanned Products</h1>
      </div>
      <div class="row">
        <label>Product Code</label>
        <input type="text" class="textbox">
      </div>
      <div class="row">
        <label>Product Name</label>
        <input type="text" class="textbox">
      </div>
      <div class="row">
        <label>Price</label>
        <input type="text" class="textbox">
      </div>
      <div class="row">
        <label>Colors</label>
        <select class="textbox">
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
        <div class="quantity-container">
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
        <input type="text" class="textbox">
      </div>
      <div class="row submit">
        <button class="submit-button"@click="submitOrder">SUBMIT</button>
      </div>
      <div class="row">
        <button class="combined-button" @click="goToHome">
          <span class="cancel-text">Cancel</span>
          <span class="separator">/</span>
          <span class="scan-text">Scan Again</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      quantity: 1, // Initialize quantity
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
  font-size: 24px;
  margin-top: -20px;
}

label {
  font-weight: 900;
}

.textbox {
  width: 100%;
  padding: 5px;
  border: 1px solid rgb(233, 161, 29); /* Orange border */
  border-radius: 5px;
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

.quantity-container {
  display: flex; /* Use flex to align items */
  width: 100%; /* Make the container full width */
  position: relative; /* Position relative for absolute positioning of arrows */
}

.quantity-input {
  flex-grow: 1; /* Make input take the available space */
  padding: 10px; /* Padding inside the input */
  text-align: center;
  border: 1px solid rgb(233, 161, 29); /* Orange border */
  border-radius: 5px;
  font-size: 16px;
}

.arrow-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.arrow-up,
.arrow-down {
  cursor: pointer;
  font-size: 20px; /* Adjust size for better visibility */
  color: rgb(233, 161, 29); /* Match arrow color with the theme */
  margin: 0; /* Remove margin */
}
  .submit-button {
    width: 50%;
    padding: 10px; /* Added padding for better button appearance */
    font-size: 16px;
    font-weight: bold;
    color: white;
    background-color: rgb(233, 161, 29);
    border: none;
    border-radius: 5px;
    cursor: pointer;
    align-self: center;
    height: auto; /* Let height adjust based on content */
  }

  .button-group {
    display: flex;
    justify-content: center;
    width: 100%;
  }

  .combined-button {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 5px; /* Space between texts */
    padding: 4px 10px; /* Padding */
    font-size: 16px;
    font-weight: bold;
    color: transparent; /* Make text transparent */
    background-color: transparent; /* No background */
    border: 2px solid orange; /* Border color */
    cursor: pointer;
    height: auto; /* Let height adjust based on content */
    width: auto;
    border-radius: 15px;
    margin: auto;
  }

  .cancel-text {
    color: gray; /* Gray color for Cancel */
  }

  .separator {
    color: rgb(233, 161, 29); /* Orange color for the slash */
  }

  .scan-text {
    color: red; /* Red color for Scan Again */
  }
</style>
