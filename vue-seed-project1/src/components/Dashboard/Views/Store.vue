<template>
    <div class="row">
      <div class="col-md-12">
        <div class="card">
          <!-- <paper-table :title="table1.title" :sub-title="table1.subTitle" :data="items.data" :columns="table1.columns"> -->

          <!-- </paper-table> -->
          <table id="firstTable" style="width:100%">
  <thead>
    <tr>
      <th>ID</th>
      <th>Name</th>
      <th>Price</th>
      <th>Seller Name</th>
      <th>CreatedAt</th>
      <th>Updated</th>
      <!-- <th class="text-right">Actions</th> -->
    </tr>
  </thead>
  <tbody>
    <tr v-for="row in myitems.data">
      <td>{{row._id}}</td>
      <td>{{row.name}}</td>
      <td>{{row.price}}</td>
      <td>{{row.sellerName}}</td>
      <td>{{row.createdAt}}</td>
      <td>{{row.updatedAt}}</td>

    <!-- <button type="button" class="close" data-dismiss="modal" aria-hidden="true">
      <span class="glyphicon glyphicon-remove" aria-hidden="true"></span></button></td> -->
    </tr>
  </tbody>
</table>
          <div>
            <br>
            <br>
            Enter  product name:
            <input v-model="name" type="text" ><br>

            Enter price:
            <input v-model="price" type="text" ><br>

            Enter  seller name:
            <input v-model="seller" type="text" ><br>

          </div>
          <button v-on:click="AddProduct"> Add Product</button>
        </div>
        <br>
        <br>
        Enter ProductId to delete:
        <input v-model="prodID" type="text" ><br>
          <button v-on:click="DeleteProduct"> Delete Product</button>
        <br>
        <br>
        Enter ProductId to update:
          <input v-model="updateID" type="text" >
          Enter name to update:
            <input v-model="updateName" type="text" >
            Enter price to update:
              <input v-model="updatePrice" type="text" ><br>
            <button v-on:click="UpdateProduct"> Update Product</button>
      </div>

    </div>
</template>
<script>

import axios from 'axios'
import PaperTable from 'components/UIComponents/PaperTable.vue'
const tableColumns = ['Id', 'Name', 'Price', 'CreatedAt', 'UpdatedAt', 'SellerName', 'Action', '']
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
      name: '',
      price: 0,
      myitems: [],
      prodID: '',
      seller: '',
      prodIDupdate: '',
      updateID: '',
      updateName: '',
      updatePrice: 0
    }
  },
  created () {
    this.GetProducts()
  },
  methods: {
    AddProduct () {
      axios.post('http://localhost:3000/api/product/createProduct', {
        name: this.name,
        price: this.price,
        sellerName: this.seller
      })
      .then((response) => {
        console.log(response)
      })
      .catch((error) => {
        console.log(error)
      })
    },
    GetProducts () {
      axios.get('http://localhost:3000/api/product/getProducts')
      .then((response) => {
        this.items = response.data
        console.log(response)
      })
      .catch((error) => {
        console.log(error)
      })
    },
    DeleteProduct () {
      axios.delete('http://localhost:3000/api/product/deleteProduct/' + this.prodID)
      .then((response) => {
        console.log(response)
      })
      .catch((error) => {
        console.log(error)
      })
    },
    UpdateProduct () {
      axios.patch('http://localhost:3000/api/product/updateProduct/' + this.updateID, {
        name: this.updateName,
        price: this.updatePrice
      })
      .then((response) => {
        console.log(response)
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
