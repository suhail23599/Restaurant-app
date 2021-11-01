<template>
   <div class="nav">
      <router-link to="/">Home</router-link>
      <router-link to="/add">Add Restaurant</router-link>
      <a @click="logout()">Logout</a>
   </div>
</template>

<script>
export default {
   name: 'Header',
   methods: {
      logout() {
         localStorage.clear()
         this.$router.push({name:'LogIn'})
      }
   }
}
</script>

<style scoped>
.nav {
   background: coral;
   height: 50px;
}
.nav a {
   font-size: 20px;
   text-decoration: none;
   color: darkblue;
   margin-top: 10px;
   float: left;
   padding-right: 20px;
}
</style>

