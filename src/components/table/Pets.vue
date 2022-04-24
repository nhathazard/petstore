<template>
  <div>
      <h1>Quản lý Pets</h1>
     
      <input class="border-2 mb-2" type="text"  v-model="searchPets">
      <table class="ml-[50px]">
          <thead class="border-y-2 border-x-2">
              <tr>
                  <th class="px-4 border-x-2 w-[140px]">ID</th>
                  <th class="px-4 border-x-2 w-[140px]">Name</th>
                  <th class="px-4 border-x-2 w-[140px] ">category</th>
                  <th class="px-4 border-x-2 w-[140px]">status</th>
              </tr>
          </thead>
          <tbody>
              <tr v-for="(pet,index) in pets " :key="index">
                  <td class="border-y-2 border-x-2">{{index}}</td>
                  <td class="border-y-2 border-x-2">{{pet.name}}</td>
                  <td class="border-y-2 border-x-2">{{pet.category?.name}}</td>
                  <td class="border-y-2 border-x-2">{{pet.status}}</td>
              </tr>
          </tbody>
      </table>
      <div class="flex flex-row">
          <div v-for="item in totalPage" :key="item" class="p-1 border cursor-pointer" :class=" {'text-red-500' : page + 1 === item}" @click="page = item -1 ">
              {{item}}
          </div>
      </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
name:"pets",
components:{
},
data(){
    return{
   pets:[],
   searchPets:'',
   page: 0,
    }
    
},
computed:{
  currentPets() {
      if (this.searchPets) {
          return this.pets.filter(pet =>{
          return pet.name.match(this.searchPets)
      })
      }
      return this.pets.slice(this.page, this.page + 10)
  },
  totalPage() {
      return Math.ceil(this.pets.length / 10)
  }
},
created(){
    axios.get('https://petstore.swagger.io/v2/user/login?username=nhat&password=123456')
    .then(response =>{
      this.pets = response.data
      console.log(this.pets)
    })
    .catch(error =>{
        console.log(error);
    })
}
}
</script>

<style>

</style>