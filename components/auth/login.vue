/* eslint-disable vue/attributes-order */
<template>
  <div id="body">
    <div class="container" id="container">
      <div class="form-container sign-in-container">
        <form @submit.prevent="logUserIn">
          <div class="mb-3" v-if="loading">
            <loader />
          </div>
          <h1 class="mb-5 text-xl">Sign in</h1>

          <div class="mb-4 mt-5">
            <label
              class="block text-gray-700 text-left text-sm font-bold mb-2"
              for="username"
              >Username</label
            >
            <input
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="username"
              type="text"
              v-model="login.username"
              placeholder="Username"
            />
          </div>
          <div class="mb-4">
            <label
              class="block text-gray-700 text-left text-sm font-bold mb-2"
              for="username"
              >Password</label
            >
            <input
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="username"
              type="password"
              v-model="login.password"
              placeholder="**********"
            />
          </div>

          <button
            class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
            type="submit"
          >
            Sign In
          </button>
        </form>
      </div>
      <div class="overlay-container">
        <div class="overlay">
          <div class="overlay-panel overlay-right">
            <h1>Hello, Friend!</h1>
            <p>Enter your personal details and start journey with us</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import swal from 'sweetalert'
import loader from '@/components/loader/loader'
import auth from '../../utils/auth'
export default {
  components: {
    loader
  },
  created() {
    if (auth.userIsLogged()) {
      this.$router.push('/login')
    }
  },
  data() {
    return {
      loading: false,
      userLoggedIn: false,
      login: {
        username: '',
        password: ''
      }
    }
  },
  methods: {
    async logUserIn() {
      this.loading = true
      try {
        let response = await this.$axios.post('admin/login', this.login)
        if (response.data.success == true) {
          let token = response.data.token
          localStorage.setItem('jwt', token)

          this.loading = false
          this.userLoggedIn = true
          if (this.userLoggedIn) {
            auth.loginUser(token)
            this.$router.push('/dashboard')
            swal('Success', 'Login Successful', 'success')
          }
        } else {
          swal('Error', 'Login Error', 'error')
        }
      } catch (err) {
        this.loading = false
        swal('Error', 'Login Error', 'error')
        console.log(err)
      }
    }
  }
}
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Montserrat:400,800');
* {
  box-sizing: border-box;
}
#body {
  background: #f6f5f7;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  font-family: 'Montserrat', sans-serif;
  height: 100vh;
  margin: -20px 0 50px;
}
h1 {
  font-weight: bold;
  margin: 0;
}
h2 {
  text-align: center;
}
p {
  font-size: 14px;
  font-weight: 100;
  line-height: 20px;
  letter-spacing: 0.5px;
  margin: 20px 0 30px;
}

span {
  font-size: 12px;
}
a {
  color: #333;
  font-size: 14px;
  text-decoration: none;
  margin: 15px 0;
}
button {
  transition: transform 80ms ease-in;
}
button:active {
  transform: scale(0.95);
}

button:focus {
  outline: none;
}

button.ghost {
  background-color: transparent;
  border-color: #ffffff;
}
form {
  background-color: #ffffff;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  padding: 0 50px;
  height: 100%;
  text-align: center;
}

.container {
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
  position: relative;
  overflow: hidden;
  width: 768px;
  max-width: 100%;
  min-height: 520px;
}
.form-container {
  position: absolute;
  top: 0;
  height: 100%;
  transition: all 0.6s ease-in-out;
}

.sign-in-container {
  left: 0;
  width: 50%;
  z-index: 2;
}

.container.right-panel-active .sign-in-container {
  transform: translateX(100%);
}
.sign-up-container {
  left: 0;
  width: 50%;
  opacity: 0;
  z-index: 1;
}

.container.right-panel-active .sign-up-container {
  transform: translateX(100%);
  opacity: 1;
  z-index: 5;
  animation: show 0.6s;
}
@keyframes show {
  0%,
  49.99% {
    opacity: 0;
    z-index: 1;
  }

  50%,
  100% {
    opacity: 1;
    z-index: 5;
  }
}
.overlay-container {
  position: absolute;
  top: 0;
  left: 50%;
  width: 50%;
  height: 100%;
  overflow: hidden;
  transition: transform 0.6s ease-in-out;
  z-index: 100;
}

.container.right-panel-active .overlay-container {
  transform: translateX(-100%);
}
.overlay {
  background: #14233b;
  background: -webkit-linear-gradient(to right, #14234d, #14233b);
  background: linear-gradient(to right, #14234d, #14233b);
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 0 0;
  color: #ffffff;
  position: relative;
  left: -100%;
  height: 100%;
  width: 200%;
  transform: translateX(0);
  transition: transform 0.6s ease-in-out;
}
.container.right-panel-active .overlay {
  transform: translateX(50%);
}

.overlay-panel {
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  padding: 0 40px;
  text-align: center;
  top: 0;
  height: 100%;
  width: 50%;
  transform: translateX(0);
  transition: transform 0.6s ease-in-out;
}
.overlay-left {
  transform: translateX(-20%);
}

.container.right-panel-active .overlay-left {
  transform: translateX(0);
}

.overlay-right {
  right: 0;
  transform: translateX(0);
}
.container.right-panel-active .overlay-right {
  transform: translateX(20%);
}

.social-container {
  margin: 20px 0;
}
.social-container a {
  border: 1px solid #dddddd;
  border-radius: 50%;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  margin: 0 5px;
  height: 40px;
  width: 40px;
}
</style>
