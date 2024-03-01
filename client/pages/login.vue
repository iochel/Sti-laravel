<template>
    <div class="login-form">
      <h2>Login</h2>
      <form @submit.prevent="handleLogin">
        <div class="form-group">
          <label for="email">Email</label>
          <input type="email" id="email" v-model="state.user.email" placeholder="Enter your email">
          <p class="error-message">{{ state.errors && state.errors._data && state.errors._data.errors && state.errors._data.errors.email && state.errors._data.errors.email[0]}}</p>
        </div>
        <div class="form-group">
          <label for="password">Password</label>
          <input type="password" id="password" v-model="state.user.password" placeholder="Enter your password">
          <p class="error-message">{{ state.errors && state.errors._data && state.errors._data.errors && state.errors._data.errors.password && state.errors._data.errors.password[0]}}</p>
        </div>
        <button type="submit">Login</button>
      </form>
    </div>
  </template>
  
  <script setup>
  import { reactive } from 'vue';
  
  const state = reactive({
    errors: null,
    user:{
      email: null,
      password: null,
    }
  });
  
  async function handleLogin(){
    const params = {
      email: state.user.email,
      password: state.user.password,
    }
  
    try {
      const response = await $fetch(`http://127.0.0.1:8000/api/auth/login`, {
        method: 'POST',
        body: params
      })
  
      if (response.data){
        localStorage.setItem('_token', response.data.token);
        navigateTo('/dashboard');
      }
    }
    catch (error){
      state.errors = error.response;
      console.log('error', error);
    }
  }
  </script>
  
  <style scoped>
  .login-form {
    max-width: 400px;
    margin: 100px auto;
    padding: 80px;
    border: 1px solid #ccc;
    border-radius: 10px;
    background-color: #4a7790;
  }
  
  h2 {
    text-align: center;
    margin-bottom: 20px;
    color: #333;
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  label {
    display: block;
    margin-bottom: 5px;
    color: #333;
  }
  
  input[type="email"],
  input[type="password"] {
    width: 100%;
    padding: 10px;
    font-size: 16px;
    border-radius: 5px;
    border: 1px solid #ccc;
  }
  
  button {
    display: block;
    width: 100%;
    padding: 10px;
    font-size: 16px;
    border-radius: 35px;
    border: none;
    background-color: #007bff;
    color: white;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  
  .error-message {
    color: #d9534f;
    font-size: 14px;
    margin-top: 5px;
  }
  
  @media (max-width: 768px) {
    .login-form {
      max-width: 300px;
    }
  }
  </style>
  