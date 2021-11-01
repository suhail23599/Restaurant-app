<template>
   <div>
      <Header></Header>
      <h1>Welcome to Add Page</h1>
      <form class="register">
         <input type="text" placeholder="Name" v-model="restaurant.name"/>
         <input type="text" placeholder="Address" v-model="restaurant.address"/>
         <input type="text" placeholder="Contact" v-model="restaurant.contact"/>
         <button type="button" @click="add()">Add New Restaurant</button>
      </form>
   </div>
</template>

<script>
import Header from '@/components/Header.vue'
import axios from 'axios'
export default {
   name: 'Add',
   components: {
      Header
   },
   data () {
      return {
         restaurant: {
            name: '',
            address: '',
            contact: ''
         }
      }
   },
   mounted () {
      if(!localStorage.getItem('user-info')) {
         this.$router.push({name: 'SignUp'})
      }
   },
   methods : {
      async add () {
         let result = await axios.post('http://localhost:3000/restaurants', this.restaurant)
         if(result.status === 201) {
            this.$router.push({name:'Home'})
         }
      }
   }
}
</script>

<style scoped>
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
