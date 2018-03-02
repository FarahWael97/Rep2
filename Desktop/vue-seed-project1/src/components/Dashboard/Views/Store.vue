<template>
     <div class="row">
       <div class="col-md-12">
         <div class="card">

          <div>
          <table style="width:100%">
              <tr>
                <th>ID</th>
                <th>Name</th>
                <th>Price</th>
                <th>CreatedAt</th>
                <th>UpdatedAt</th>
                <th>SellerName</th>
              </tr>
              <tr v-for="row in rows.data">
                 <td>{{row._id}}</td>
                <td>{{ row.name }}</td>
                <td>{{ row.price }}</td>
               <td>{{row.createdAt}}</td>
               <td>{{row.updatedAt}}</td>
               <td>{{row.sellername}}</td>
               </tr>
          </table>
          </div>
         </div>
         Enter prodID to del:
         <input v-model= "pID" type= "text">
         <br>
         <button v-on:click="deleteProd">Delete!</button>
         <br>
         Enter name to create:
         <input v-model= "pName" type= "text">
         Enter price to create:
         <input v-model= "pPrice" type= "text">
         <br>
         <button v-on:click="createProd">Create!</button>
         <br>
         Enter uID to update:
         <input v-model= "uID1" type= "text">
         Enter name to update:
         <input v-model= "uName1" type= "text">
         Enter price to update:
         <input v-model= "uPrice1" type= "text">
         <br>
         <button v-on:click="updateProd">Update!</button>
         <br>
       </div>
     </div>
</template>
<script>
import axios from 'axios'
import PaperTable from 'components/UIComponents/PaperTable.vue'
const tableColumns = ['Id', 'Name', 'Price', 'CreatedAt', 'UpdatedAt', 'SellerName', '']
const tableData = [{
  id: 1,
  name: 'Dakota Rice',
  price: '$36.738',
  createdat: '15/2/2018',
  updatedat: '16/2/2018',
  sellername: 'Mo'
},
{
  id: 2,
  name: 'Minerva Hooper',
  price: '$36.738',
  createdat: '15/2/2018',
  updatedat: '16/2/2018',
  sellername: 'Mo'
}]
export default {
  components: {
    PaperTable
  },
  data () {
    return {
      table1: {
        title: 'Stripped Table',
        subTitle: 'Here is a subtitle for this table',
        columns: [...tableColumns],
        data: [...tableData]
      },
      table2: {
        title: 'Table on Plain Background',
        subTitle: 'Here is a subtitle for this table',
        columns: [...tableColumns],
        data: [...tableData]
      },
      rows: [],
      pID: '',
      pName: '',
      pPrice: '',
      uID1: '',
      uName1: '',
      uPrice1: ''
    }
  },
  created () {
    this.gettingProd()
  },
  methods: {
    AddToApi () {
      axios.post('http://localhost:3000/User')
    .then((response) => {
      console.log(response)
    })
    .catch((error) => {
      console.log(error)
    })
    },
    gettingProd () {
      axios.get('http://localhost:3000/api/product/getProducts')
      .then((response) => {
        this.rows = response.data
        console.log(this.rows)
      })
      .catch((error) => {
        console.log(error)
      })
    },
    deleteProd () {
      axios.delete('http://localhost:3000/api/product/deleteProduct/' + this.pID)
      .then((response) => {
        console.log(this.rows)
      })
      .catch((error) => {
        console.log(error)
      })
    },
    createProd () {
      axios.post('http://localhost:3000/api/product/createProduct', {
        name: this.pName,
        price: this.pPrice
      })
      .then((response) => {
        console.log(this.rows)
      })
      .catch((error) => {
        console.log(error)
      })
    },
    updateProd () {
      axios.patch('http://localhost:3000/api/product/updateProduct/' + this.uID1, {
        name: this.uName1,
        price: this.uPrice1
      })
      .then((response) => {
        console.log(this.rows)
      })
      .catch((error) => {
        console.log(error)
      })
    }
  }
}

</script>
<style>

</style>
