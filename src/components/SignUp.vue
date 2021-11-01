<template>
<div>
   <img src="@/assets/rest-logo.jpeg" alt="logo" class="logo">
   <h1>Join Us</h1>
   <div class="register">
      <input type="text" placeholder="Name" v-model="name"/>
      <input type="email" placeholder="Email" v-model="email"/>
      <input type="password" placeholder="Password" v-model="password"/>
      <button type="submit" @click="submit()">Submit</button>
      <p>
         <router-link to="/login">Login Page</router-link>
      </p>
   </div>
</div>
</template>

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

<script>
import axios from 'axios'
export default {
   name: 'signUp',
   data() {
      return {
         name: '',
         email: '',
         password:''
      }
   },
   mounted () {
      if (localStorage.getItem('user-info')) {
         this.$router.push({name:'Home'})
      }
   },
   methods: {
      async submit () {
         let request = {
            name: this.name,
            email: this.email,
            password: this.password
         }
         let result = await axios.post('http://localhost:3000/users', request)
         if (result.status === 201) {
           localStorage.setItem('user-info', JSON.stringify(result.data))
           this.$router.push({name:'Home'})
         }
      }
   }
}
</script>

