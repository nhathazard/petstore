<template>
  <Pets :columns="columns" :entries="entries" />
</template>

<script>
import Pets from '../Pets.vue'
export default {
    name:'DataTable',
  components: { Pets },
  data(){
      return{
          columns:[
              {name:'id', text:'ID'},
               {name:'name', text:'Name'},
                {name:'category', text:'Category'},
                 {name:'status', text:'Status'},
          ],
          entries:[]
      }

  },
  created(){
    axios.get('https://petstore.swagger.io/v2/pet/findByStatus?status=available')
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