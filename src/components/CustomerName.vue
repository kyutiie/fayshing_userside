<template>
  <div class="login-container">
    <div class="login-box">
      <img src="../assets/logo_orange.png" alt="Fayshing Hardware Logo" class="logo" />
      <h6>Please Enter Customer Information</h6>
      <form @submit.prevent="handleSubmit">
        <label for="customerName">Customer Name</label>
        <input type="text" id="customerName" v-model="customerName" placeholder="Enter Customer Name" required />

        <label for="contactNumber">Contact Number</label>
        <input type="tel" id="contactNumber" v-model="contactNumber" placeholder="Enter Contact Number" required />

        <button type="submit" class="submit-btn">SUBMIT</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      customerName: '',
      contactNumber: ''
    };
  },
  methods: {
    handleSubmit() {
      if (this.customerName && this.contactNumber) {
        console.log('Customer Name:', this.customerName);
        console.log('Contact Number:', this.contactNumber);
        // Navigate to the home page or another page after submission
        this.$router.push('/home');
      }
    }
  }
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Oswald', sans-serif;
  font-weight: bold;
}

body {
  background-color: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100%;
  position: relative;
  overflow: hidden;
}

.login-box {
  background-color: white;
  padding: 30px 100px;
  border-radius: 20px;
  border: 3px solid #ff914d;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  text-align: center;
  width: 550px;
  margin-top: 50px;
  position: relative;
  z-index: 1;
}

.logo {
  width: 280px;
  margin-bottom: 20px;
}

form {
  display: flex;
  flex-direction: column;
}

label {
  margin-bottom: -10px;
  text-align: left;
}
h6{
  margin-bottom: 20px;
}

input[type="text"],
input[type="tel"] {
  width: 100%;
  padding: 10px;
  margin-bottom: 50px;
  margin-top: 15px;
  border: 2px solid #ff914d;
  border-radius: 10px;
  outline: none;
}

input[type="text"]::placeholder,
input[type="tel"]::placeholder {
  color: #ebab83;
}
.submit-btn {
  background-color: #ff914d;
  color: white;
  padding: 0 15px; /* Adjust padding to make the button smaller */
  border: none;
  border-radius: 10px;
  cursor: pointer;
  font-weight: bold;
  font-size: 16px; /* Set font size to 16px */
  width: auto; /* Adjust width to fit the smaller button */
  margin: 0 auto;
  margin-top: 10px;
  margin-bottom: 15px;
  transition: background 0.3s ease;
}

.submit-btn:hover {
  background-color: #e2600f;
}

.link {
  display: inline-block;
  margin-top: 10px;
  color: #d86925;
  text-decoration: none;
  font-weight: normal;
}

.link:hover {
  text-decoration: underline;
}

@media (max-width: 740px) {
  .login-box {
    padding: 30px 20px;
    width: 90%;
    margin-top: 20px;
  }

  .logo {
    width: 70%;
    max-width: 200px;
  }
  .submit-btn {
    margin-top: -20px;
   
  }
 
}

</style>
