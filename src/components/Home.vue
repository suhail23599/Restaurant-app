<template>
   <div>
      <Header></Header>
      <h1>Welcome to Home Page</h1>
      <table border="1">
         <tr>
            <td>Id</td>
            <td>Name</td>
            <td>Contact</td>
            <td>Address</td>
            <td>Action</td>
         </tr>
         <tr v-for="item in restaurants" :key="item.id">
            <td>{{item.id}}</td>
            <td>{{item.name}}</td>
            <td>{{item.contact}}</td>
            <td>{{item.address}}</td>
            <td><router-link :to="'/update/'+item.id">Update</router-link></td>
            <td><button @click="deleteItem(item.id)">Delete</button></td>
         </tr>
      </table>
   </div>
</template>

<style scoped>
td {
   width: 160px;
   height: 40px;
}
</style>

<script>
import Header from '@/components/Header.vue'
import axios from 'axios'
export default {
   name: 'Home',
   components: {
      Header
   },
   data () {
      return {
         restaurants: []
      }
   },
   methods: {
      async deleteItem (id) {
         let result = await axios.delete(`http://localhost:3000/restaurants/${id}`)
         console.log(result)
         if(result.status == 200) {
            this.loadData()
         }
      },
      async loadData() {
         let result = await axios.get("http://localhost:3000/restaurants")
         this.restaurants = result.data
      }
   },
   mounted () {
      if(!localStorage.getItem('user-info')) {
         this.$router.push({name: 'SignUp'})
      }
      this.loadData()
   }
}
</script>
