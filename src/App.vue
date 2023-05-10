<template>
  <div id="logIn">

    <div class="container">

      <div class="logo">
        <h1><i class="fa-regular fa-user"></i></h1>
      </div>

      <div class="defination">
        <h2> LogIn </h2>
      </div>

      <form>
        <input type="text" placeholder="Name" v-model="user_name">
        <div class="pass">
          <input :type="fieldType" placeholder="Password" v-model="user_password">
          <i :class="f_icon" @click="changeIcon()"></i>
        </div>
        <button @click.prevent="onLogIn()">LogIn</button>
      </form>

      <div class="options">
        <label>
          <input type="checkbox" name="remember" value="true">
          <p>Remember Me</p>
        </label>
        <span><a href="#">Forgot Password</a></span>
      </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'App',
  data() {
    return {
      user_name: '',
      user_password: '',
      fieldType: 'password',
      f_icon: 'fa-solid fa-eye'
    }
  },
  methods: {
    changeIcon() {
      if (this.f_icon === 'fa-solid fa-eye' && this.fieldType === 'password') {
        this.fieldType = 'text';
        this.f_icon = 'fa-solid fa-eye-slash';
      }
      else {
        this.fieldType = 'password';
        this.f_icon = 'fa-solid fa-eye';
      }
    },
    async onLogIn() {
      const res = await axios.get(`http://localhost:3000/users?user_name=${this.user_name}&user_password=${this.user_password}`);
      console.log(res);
      if (res.status === 200 && res.data.some(user => user.user_name === this.user_name && user.user_password === this.user_password)) {
        window.alert(`Submit successfully\nHello!! ${this.user_name}`);
        window.open('https://minplan.org/' ,'_blank');
      } else {
        window.alert(`Error\nInvalid username or password`);
      }
    }
  }
}
</script>

<style>
* {
  font-weight: 700 !important;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body {
  background-color: #fff;
  font-family: Georgia, 'Times New Roman', Times, serif;
}

#logIn {
  height: 85vh;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

#logIn .container {
  width: 300px;
  padding: 2rem 0;
  border: 3px solid #42c0b7;
  border-bottom: 0;
  border-top: 0;
  border-radius: 20px;
  background: rgba(255, 255, 255, 0.24);
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(6.6px);
  -webkit-backdrop-filter: blur(6.6px);
}

#logIn .container .logo h1 {
  padding: 0.5rem;
}

#logIn .container .logo h1 i {
  padding: 0.82rem 1rem;
  border-radius: 50%;
  background-color: #42c0b7;
  color: #fff;
}

#logIn .container .defination h2 {
  font-size: 30px;
  padding: 0 0 1rem 0;
  color: #1f1f1f;
  opacity: 0.8;
}

#logIn .container form {
  margin: auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 300px;
}

#logIn .container form input,
#logIn .container form button {
  width: 250px;
  margin: 5px 0;
  padding: 0.5rem 0;
}

#logIn .container form button {
  background-color: #42c0b7;
  font-family: Georgia, 'Times New Roman', Times, serif;
  font-size: 16px;
  color: #1f1f1f;
  opacity: 0.9;
  border: 5px solid #42c0b7;
  cursor: pointer;
}

#logIn .container form button:hover {
  background-color: #42c0b7;
  border: 5px solid #42c0b7;
}

#logIn .container form input {
  border: 2px solid #1f1f1f4d;
}

#logIn .container form input:focus {
  outline: 2px solid #42c0b7;
  border: 0;
}

#logIn .container form input::placeholder {
  font-family: Georgia, 'Times New Roman', Times, serif;
  opacity: 0.8;
}

#logIn .container form .pass {
  position: relative;
}

#logIn .container form i {
  position: absolute;
  top: 35%;
  right: 5px;
  color: #42c0b7;
  opacity: 0.6;
  cursor: pointer;
}

/*end container*/
#logIn .options {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-evenly;
  font-size: 14px;
  width: 100%;
  padding: 1rem 0 0 0;
}

#logIn .options label {
  display: flex;
  align-items: center;
  justify-content: center;
}

#logIn .options label input[type="checkbox"] {
  accent-color: #42c0b7 !important;
}

#logIn .options span a {
  color: #1f1f1f;
  text-decoration: unset;
}

#logIn .options span a:hover {
  color: #42c0b7;
}
</style>
