<template>
    <div class="product_info">
        <div class="pricing-header px-3 py-3 pt-md-5 pb-md-4 mx-auto text-center">
            <h3 class="display-5">Product Infomation</h3>
            <router-link to="/products">Back</router-link>
        </div>

        <div class="container">
            <form @submit.prevent="save()">
                <div class="form-group row">
                    <label for="inputPassword" class="col-sm-3 col-form-label">Product name</label>
                    <div class="col-sm-9">
                        <input v-bind:class="{ 'is-invalid': error.name }" type="text" class="form-control"
                            @blur="validation()" v-model="product.name" />
                        <i style="display: block;" class="text-left text-xs text-red-500">{{ error.name }}</i>
                    </div>
                </div>
                <div class="form-group row">
                    <label for="inputPassword" class="col-sm-3 col-form-label">Product price</label>
                    <div class="col-sm-9">
                        <input v-bind:class="{ 'is-invalid': error.price }" type="text" class="form-control"
                            v-model="product.price" />
                        <i style="display: block;" class="text-left text-xs text-red-500">{{ error.price }}</i>
                    </div>
                </div>
                <div class="form-group row">
                    <label for="inputPassword" class="col-sm-3 col-form-label">Product description</label>
                    <div class="col-sm-9">
                        <textarea @blur="validation()" v-bind:class="{ 'is-invalid': error.description }"
                            class="form-control" rows="3" v-model="product.description"></textarea>
                        <i style="display: block;" class="text-left text-xs text-red-500">{{ error.description }}</i>
                    </div>
                </div>
                <div class="form-group row">
                    <label for="inputPassword" class="col-sm-3 col-form-label"></label>
                    <div class="col-sm-9 text-left">
                        <button type="submit" class="btn btn-primary">Save</button> &nbsp;
                        <button type="reset" class="btn btn-danger">Cancel</button>
                    </div>
                </div>
            </form>
        </div>
    </div>
</template>
<script>
export default {
    // name: 'ProductForm',
    data() {
        return {
            error: {
                name: '',
                price: '',
                description: ''
            },
            product: {
                name: '',
                price: '',
                description: ''
            }
        }
    },
    methods: {
        validation() {
            this.error = {
                name: '',
                price: '',
                description: ''
            }
            if (!this.product.name) {
                this.error.name = 'Please enter name.....';
            }
            if (!this.product.price) {
                this.error.price = 'Please enter price.....';
            }
            else if (this.product.price && typeof this.product.price !== 'number') {
                this.error.price = 'Price must be number';
            }
            if (!this.product.description) {
                this.error.description = 'Please enter des.....';
            }
            if (this.error.name === '' && this.error.price === '' && this.error.description === '') {
                return true;
            }
        },
        save() {
            if (this.validation()) {

            }
        }
    }
}
</script>