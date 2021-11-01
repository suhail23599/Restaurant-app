<template>
   <div>
      <Header></Header>
      <h1>Welcome to Update Page</h1>
      <form class="register">
         <input type="text" placeholder="Name" v-model="restaurant.name"/>
         <input type="text" placeholder="Address" v-model="restaurant.address"/>
         <input type="text" placeholder="Contact" v-model="restaurant.contact"/>
         <button type="button" @click="update()">Update Restaurant</button>
      </form>
   </div>
</template>

<script>
import Header from '@/components/Header.vue'
import axios from 'axios'
export default {
   name: 'Update',
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
   methods: {
      async update () {
         let result = await axios.put(`http://localhost:3000/restaurants/${this.$route.params.id}`, this.restaurant)
         if(result.status === 200) {
            this.$router.push({name:'Home'})
         }
      }
   },
   async mounted () {
      if(!localStorage.getItem('user-info')) {
         this.$router.push({name: 'SignUp'})
      }
      let id = this.$route.params.id
      let result = await axios.get(`http://localhost:3000/restaurants/${id}`)
      this.restaurant = result.data
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
