<template>
    <div class="background">
        <div class="container">
            <div class="row logo">
                <img src="../assets/logo_orange.png" alt="Logo">
            </div>
            <div class="row title">
                <h1>Ordered Products</h1>
            </div>
            <div class="row">
                <input type="text" class="textbox" placeholder="Name of Client">
            </div>

            <div class="product-container">
                <div class="product-row" v-for="(product, index) in products" :key="index">
                    <div class="product-col col1">
                        <div class="product-name">{{ product.name }}</div>
                        <div class="product-size">{{ product.size }} mm</div>
                    </div>
                    <div class="product-col col2">{{ product.price }}</div>
                    <div class="product-col col3">
                        <div class="quantitycontainer">
                            <input type="text" class="quantity-input" v-model="product.quantity" readonly>
                            <div class="arrow-container">
                                <button @click="increaseQuantity(product)" class="arrow-button arrow-up">▲</button>
                                <button @click="decreaseQuantity(product)" class="arrow-button arrow-down">▼</button>
                            </div>
                        </div>
                    </div>
                    <div class="product-col col4">{{ product.quantity * product.price }}</div>
                    <div class="product-col col5">
                        <button @click="deleteProduct(index)" class="delete-icon">🗑️</button>
                    </div>
                </div>
            </div>

            <div class="row">
                <button class="combined-button" @click="goToHome">
                    <span class="scan-text">Scan Again</span>
                </button>
            </div>

            <!-- Total Price Section -->
            <div class="total-section">
                <label for="totalPrice">Total Price</label>
                <input type="text" id="totalPrice" class="textbox" v-model="totalPrice" readonly>
            </div>

            <!-- Submit Button -->
            <div class="submit-container">
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
                { name: 'Product 1', size: 10, price: 100, quantity: 1 },
                { name: 'Product 2', size: 20, price: 150, quantity: 1 },
            ],
        };
    },
    computed: {
        totalPrice() {
            return this.products.reduce((total, product) => {
                return total + (product.price * product.quantity);
            }, 0);
        },
    },
    methods: {
        increaseQuantity(product) {
            product.quantity++;
        },
        decreaseQuantity(product) {
            if (product.quantity > 1) {
                product.quantity--;
            }
        },
        deleteProduct(index) {
            this.products.splice(index, 1);
        },
        submitOrder() {
            // Navigate to the payment page
            this.$router.push('/payment');
        },
        goToHome() {
            this.$router.push('/home');
        },
    }
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
    width: calc(100% - 20px);
    height: calc(100% - 20px);
    background-color: white;
    border: 2px solid rgb(233, 161, 29);
    border-radius: 20px;
    box-sizing: border-box;
    padding: 15px 50px;
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
    font-size: 24px;
    margin-top: -20px;
}

.textbox {
    width: 100%;
    padding: 5px;
    border: 1px solid rgb(233, 161, 29);
    border-radius: 5px;
    font-size: 16px;
}

.product-container {
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin-top: 3px;
}

.product-row {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr 1fr 0.5fr; /* Columns for product layout */
    align-items: center;
    background-color: #f9f9f9; /* Light background for products */
    padding: 0px 5px;
    border: 1px solid rgb(233, 161, 29);
    border-radius: 10px;
    font-weight: bold;
    color: #474343;
    margin-top: 10px;
}

.product-col {
    padding: 5px;
}

.col1 {
    display: flex;
    flex-direction: column; /* Stack product name and size vertically */
    width: 80px;
}

.product-name {
    font-weight: bold;
}

.product-size {
    font-size: 12px;
    color: #555;
}

.quantity-container {
    display: flex;
    align-items: center;
    position: relative; /* To position the arrows inside */
}

.quantity-input {
    width: 50px; /* Fixed width for quantity input */
    text-align: left;
    border: 1px solid rgb(233, 161, 29);
    border-radius: 5px;
    padding: 7px;
    font-size: 14px;
    position: relative; /* To position arrows inside */
}

.arrow-container {
    display: flex;
    flex-direction: column; /* Stack the arrows vertically */
    position: absolute; /* Absolute positioning for arrows */
    right: 5px; /* Position arrows inside the input box */
    top: 0; /* Align to the top */
    gap: 0; /* No gap between the arrows */
    margin-top: 19px;
}

.arrow-button {
    color: rgb(241, 180, 12); /* Text color for arrows */
    border: none;
    border-radius: 5px;
    cursor: pointer; /* Pointer cursor on hover */
    padding: 2px; /* Smaller padding for compactness */
    font-size: 10px; /* Smaller font size for arrows */
    width: 20px; /* Fixed width for arrows */
    height: 20px; /* Fixed height for arrows */
    line-height: 0; /* Line height adjustment */
    margin-top: -7px;
}

.delete-icon {
    cursor: pointer;
    border: none;
    background: none;
    color: rgb(233, 161, 29);
    font-size: 20px;
}

.total-section {
    display: flex;
    align-items: center;
    justify-content: space-between; /* Space between label and input */
    width: 100%; /* Full width */
    margin-top: 180px; /* Space above total section */
}

.total-section label {
    font-weight: bold; /* Bold label text */
}

.total-section .textbox {
    padding: 8px;
    border: 1px solid rgb(233, 161, 29); /* Orange border */
    border-radius: 5px;
    width: 100%; /* Takes up remaining space */
    max-width: 200px; /* Limits input width */
    height: 25px;
    box-sizing: border-box;
}

.submit-container {
    display: flex;
    justify-content: flex-end; /* Aligns the button to the right */
    width: 100%; /* Ensures the container takes full width of its parent */
    margin-top: 10px; /* Adds space above the button */
    margin-left:150px;
}

.submit-button {
    background-color: #ff914d;
    color: white;
    border: none;
    border-radius: 5px;
    padding: 5px 30px;
    font-size: 14px;
    cursor: pointer;
    width: auto; /* Adjusts width to fit content */
}

.submit-button:hover {
    background-color: rgb(241, 180, 12);
}

.combined-button {
    border: 1px solid #ff914d; /* 2px solid border with specified color */
    border-radius: 20px; /* Rounded corners */
    padding: 5px 40px; /* Padding for vertical and horizontal spacing */
    background-color: white; /* Optional: background color */
    color: #ff914d; /* Text color */
    font-weight: bold; /* Bold text */
    cursor: pointer; /* Pointer cursor on hover */
    text-align: center; /* Centered text */
    width: 100%; /* Full width */
    height: 30px; /* Fixed height */
}

.scan-text {
    font-size: 14px; /* Font size for text */
    padding: 10px; /* Padding around the text */
}

.combined-button:hover {
    background-color: #ff914d; /* Change background on hover */
    color: white; /* Change text color on hover */
}
</style>
