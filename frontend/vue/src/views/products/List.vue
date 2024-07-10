<template>
    <div class="products_list">
        <div class="pricing-header px-3 py-3 pt-md-5 pb-md-4 mx-auto text-center">
            <h2 class="display-4">Product Management</h2>
            <p><a href="/product/create">Add new</a></p>
          </div>
          <div class="container">
            <div class="card-deck mb-3 text-center">
              <table class="table table-bordered">
                <thead>
                  <tr>
                    <th scope="col">#</th>
                    <th scope="col">Product name</th>
                    <th scope="col">Price</th>
                    <th scope="col">Handle</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(product,index) in products">
                    <th scope="row">{{index + 1}}</th>
                    <td>{{ product.name}}</td>
                    <td>{{ product.price}}</td>
                    <td>
                      <router-link :to="{ name: 'product.edit', params: {id: product.id}}">
                        <button class="btn btn-primary mr-1">Edit</button>
                      </router-link>
                      <button @click="this.delete(product.id)" class="btn btn-danger">Delete</button>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
    </div>
</template>

<script>
import router from '@/router';

export default {
  data() {
    return {
      products: []
    }
  },
  created() {
    this.getAll();
  },
  methods: {
    getAll() {
      this.$request.get('http://localhost:8000/api/products').then(res => {
        this.products = res.data;
      })
    },
    delete(id) {
      this.$request.delete(`http://localhost:8000/api/products/${id}`).then(res => {
        if(res.data.success){
          this.getAll();
        } else {
          alert("Can't delete this product")
        }
      })
    }
  }
}
</script>