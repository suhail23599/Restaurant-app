<template>
   <div>
   <img src="@/assets/rest-logo.jpeg" alt="logo" class="logo">
   <h1>Log In</h1>
   <div class="register">
      <input type="email" placeholder="Email" v-model="email"/>
      <input type="password" placeholder="Password" v-model="password"/>
      <button type="submit" @click="login()">Log  In</button>
      <p>
         <router-link to="/signup">SignUp Page</router-link>
      </p>
   </div>
   </div>
</template>

<script> 
import axios from 'axios'
export default {
   name: 'LogIn',
   data () {
      return {
         email: '',
         password: ''
      }
   },
   mounted () {
      if (localStorage.getItem('user-info')) {
         this.$router.push({name:'Home'})
      }
   },
   methods: {
      async login () {
         let result = await axios.get(`http://localhost:3000/users?email=${this.email}&password=${this.password}`)
         if (result.status == 200 && result.data.length) {
            localStorage.setItem('user-info', JSON.stringify(result.data))
            this.$router.push({name:'Home'})
         }
      }
   }
}
</script>
<style scoped>
.logo {
  height: 20vh;
}
.register {
   display: flex;
   flex-direction: column;
   gap: 30px;
   align-items: center;
}
input, button {
   width: 200px;
   height: 30px;
   border: 1px solid skyblue;
}
</style>