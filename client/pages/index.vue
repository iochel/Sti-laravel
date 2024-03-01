<template>
  <div class="navigation-container">
    <div class="navigation-card" @click="goTo('/login')">
      <h3>Log In</h3>
      <p>Click here to log in to your account</p>
    </div>
    <div class="navigation-card" @click="goTo('/register')">
      <h3>Sign Up</h3>
      <p>Click here to create a new account</p>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    goTo(path) {
      this.$router.push(path);
    }
  }
}
</script>

<style scoped>
.navigation-container {
  display: flex;
  justify-content: space-around;
}

.navigation-card {
  width: 350px;
  padding: 60px;
  margin: 120px;
  border: 1px solid #ccc;
  border-radius: 8px;
  background-color: #f9f9f9;
  cursor: pointer;
  transition: all 0.3s ease;
}

.navigation-card:hover {
  transform: translateY(-5px);
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
}

.navigation-card h3 {
  margin-bottom: 10px;
  color: #333;
}

.navigation-card p {
  color: #666;
}
</style>
