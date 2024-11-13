<template>
  <div class="mpin">
    <div class="top-half">
      <img src="../assets/logo_white.png" alt="logo Image" class="logo" />
      <div class="user-dropdown-container">
        <select v-model="selectedUser" class="dropdown">
          <option value="user1">User 1</option>
          <option value="user2">User 2</option>
        </select>
      </div>
      <div class="mpin-circles">
        <div 
          v-for="i in 4" 
          :key="i" 
          class="circle" 
          :class="{ filled: i <= mpin.length }">
        </div>
      </div>
      <p class="note">Enter your MPIN provided by Admin</p>
    </div>
    <div class="bottom-half">
      <div class="number-pad">
        <button 
          v-for="number in numbers.slice(0, 9)" 
          :key="number" 
          @click="appendNumber(number)">
          {{ number }}
        </button>
        <button class="zero-button" @click="appendNumber(0)">0</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedUser: 'user1',
      mpin: '',
      numbers: [1, 2, 3, 4, 5, 6, 7, 8, 9, 0],
    };
  },
  methods: {
    appendNumber(number) {
      if (this.mpin.length < 4) {
        this.mpin += number;
        if (this.mpin.length === 4) {
          this.goToHome();
        }
      }
    },
    goToHome() {
      this.$router.push('/home');
    },
  },
};
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
  overflow: hidden; 
}

.mpin {
  height: 100vh;
  display: flex;
  flex-direction: column;
  background-color: white;
}

.top-half {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start; /* Start aligning from the top */
  background: url('../assets/bg.png') no-repeat center;
  background-size: cover;
  position: relative; /* Relative position for z-index usage */
  padding: 20px 0; /* Add padding for spacing */
}

.logo {
  width: 60%;
  margin-bottom: 10px;
  margin-top: 50px;
}

.user-dropdown-container {
  display: flex;
  justify-content: center;
  margin-bottom: 10px; /* Space between dropdown and circles */
}

.dropdown {
  border: 2px solid white;
  border-radius: 20px;
  background-color: #ff914d; /* Orange background */
  color: white; /* White text */
  padding: 2px 10px; /* Add padding for better spacing */
  width: 190px; /* Adjust width if necessary */
  font-size: 16px;
  font-weight: 800;
}

.mpin-circles {
  display: flex;
  gap: 30px;
  margin-top: 15px; /* Space between circles and note */
}

.circle {
  width: 14px;
  height: 14px;
  border-radius: 50%;
  border: 2px solid rgb(245, 241, 241); /* Optional: change border color if needed */
  background-color: transparent; /* Default background for empty circles */
}

.filled {
  background-color: rgb(252, 252, 252); /* Change filled circle color */
}

.note {
  margin-top: auto; /* Push the note to the bottom */
  text-align: center; /* Center the note */
  font-size: 75%;
  font-weight: 700;
  color: azure;
  padding: 10px;  
}

.bottom-half {
  flex: 1;
  background-color: white;
  border-top-left-radius: 15px; /* Round corners */
  border-top-right-radius: 15px; /* Round corners */
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: -30px; /* Overlap with the top half */
  position: relative; /* Allows stacking of elements */
}

.number-pad {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 25px;
  justify-items: center;
  align-items: center; /* Center items vertically */
}

button {
  width: 60px;
  height: 60px;
  font-size: 28px;
  background: none;
  border: none;
  cursor: pointer; 
  color: #f38925; 
  font-weight: 900;
}

button:hover {
  background-color: lightgray; /* Optional: add hover effect */
}

/* Style for the zero button */
.zero-button {
  grid-column: span 3; /* Make the zero button span across all columns */
  width: 100%; /* Ensure it takes full width */
  height: 60px; /* Match the height of other buttons */
  color: #f38925; /* Keep the number color consistent */
  font-size: 28px; /* Keep font size consistent */
  font-weight: 900; /* Keep font weight consistent */
}
</style>
