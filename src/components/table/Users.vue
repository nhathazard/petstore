<template>
  <div>
      <form @submit.prevent="addUser">
          <div class="form-group">
           <label for="name">Name:</label>
           <input type="text" v-model="formData.name" @keyup="addUser" class="form-control mt-2 border-slate-400 border-2">
          </div>
            <div class="form-group">
           <label for="name">UserName:</label>
           <input v-model="formData.username" type="text" class="form-control mt-2 mr-[31px] border-slate-400 border-2">
          </div>
            <div class="form-group">
           <label for="name">Email:</label>
           <input v-model="formData.email" type="text" class="form-control mt-2 border-slate-400 border-2">
          </div>
            <div class="form-group">
           <label for="name">Phone:</label>
           <input v-model="formData.phone" type="text" class="form-control mt-2 border-slate-400 border-2">
          </div>
            <button  class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
  Submit
</button>
      </form>
       
       <table class="ml-[50px]">
          <thead class="border-y-2 border-x-2">
              <tr>
                  <th class="px-4 border-x-2 w-[140px]">ID</th>
                  <th class="px-4 border-x-2 w-[140px]">Name</th>
                  <th class="px-4 border-x-2 w-[140px] ">UserName</th>
                  <th class="px-4 border-x-2 w-[140px]">Email</th>
                  <th class="px-4 border-x-2 w-[140px]">Phone</th>
                   <th class="px-4 border-x-2 w-[140px]">Action</th>
              </tr>
          </thead>
          <tbody>
              <tr v-for="user in users " :key="user.id">
                  <td class="border-y-2 border-x-2">{{user.id}}</td>
                  <td class="border-y-2 border-x-2">{{user.name}}</td>
                  <td class="border-y-2 border-x-2">{{user.username}}</td>
                  <td class="border-y-2 border-x-2">{{user.email}}</td>
                   <td class="border-y-2 border-x-2">{{user.phone}}</td>
                    <td  class="border-y-2 border-x-2"><button @click="deleteUser(user.id)" class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded">Delete</button></td>
              </tr>
          </tbody>
      </table>
  </div>
</template>

<script>
import axios from 'axios'
export default {
name:'users',
data(){
    return{
      users:[],
      formData:{
          name: "",
          username: "",
          email: "",
          phone: "",
      }
    }
},
methods: {
//  async addUser(){
//      const res = await axios.post('https://jsonplaceholder.typicode.com/users',{name:this.Name,username:this.UserName,email:this.Email,phone:this.Phone});
//      this.users = [...this.users,res.data]
//      this.Name = '';
//      this.UserName = '';
//      this.Email = '';
//      this.Phone = '';
//  },
addUser(){
 axios.post('https://jsonplaceholder.typicode.com/users', this.formData)
   .then(response => console.log(response))
   .catch(error => console.log(error))
 
},
deleteUser(id){
    axios.delete(`https://jsonplaceholder.typicode.com/users/id`)
    .then(response =>{
        console.log(response);
    })
}
// clickAdd(){
//     this.$emit("save", this.user)
//     this.users.push(this.user)
// },
},
 async created(){
     try {
         const res = await axios.get('https://jsonplaceholder.typicode.com/users');
         this.users = res.data;
         console.log(this.users);
     }
     catch(e){
         console.log(e);
     }
 }
}
</script>

<style>

</style>