<template>
    <div id="container-create-pet">
        <div class="header-create-pet">
            <h3>Pet Depot Checkout</h3>
        </div>
        <div id="form-create-pet">
            <h3>Enter your informations</h3>
            <div class="row">
                <div class="form-group">
                    <label for="title">Title: </label>
                    <input type="text" id="title" name="title" v-model="title" v-on:keyup="keyMonitorCheckEmpty">
                </div>
                <div class="form-group">
                    <label for="description">Description: </label>
                    <input type="text" id="description" name="description" v-model="description" v-on:keyup="keyMonitorCheckEmpty">
                </div>
            </div>
            <div class="row">
                <div class="form-group">
                    <label for="image-url">Image: </label>
                    <input type="text" id="image-url" name="image-url" v-model="image" v-on:keyup="keyMonitorCheckEmpty">
                </div>
                <div class="form-group">
                    <label for="description">Price: </label>
                    <input type="number" id="price" name="price" v-model="price" v-on:keyup="keyMonitorPrice">
                </div>
            </div>
            <div class="checkbox-group">
                <label for="visible">Visible: </label>
                <input type="checkbox" id="visible" name="visible" v-model="visible">
            </div>
            <div id="pre-data" v-if="visible">
                <Product :title="title" :description="description" :image="image" :price="price" :isPreview="isPreview" />
            </div>
            <div id="container_messages_errors">
                <ul v-for="msg_err in errors_messages" :key="msg_err">
                    <li>{{ msg_err }}</li>
                </ul>
            </div>
            <div class="container-vertical-center">
                <button class="custom-button-blue" @click="createProduct">Create product</button>
            </div>
        </div>
    </div>
</template>

<script>
import Product from './Product.vue';

export default {
    name: 'FormCreatePet',
    components: {
        Product,
    },
    data() {
        return {
            title: '',
            description: '',
            image: '',
            visible: false,
            price: 0,
            isPreview: true,
            isOkForCreate: false,
            errors_messages: [],
        }
    },
    props: ['create'],
    methods: {
        createProduct(event) {
            this.errors_messages = [];
            if (this.title.length === 0) 
                this.errors_messages.push('title is empty !');
            if (this.description.length === 0)
                this.errors_messages.push('description is empty !');
            if (this.image.length === 0) 
                this.errors_messages.push('image-url is empty !');
            if (this.price < 10)
                this.errors_messages.push('The price is too small !') 
            if (this.price > 2000) 
                this.errors_messages.push('The price is too big !')
            if (this.errors_messages.length === 0)
                this.create(this.title, this.description, this.image, this.price, this.visible);
        },

        keyMonitorPrice(event) {
            if (event.target.name === "price") {
                if (event.target.value  < 10 && this.errors_messages.indexOf('The price is too small !') === -1)
                    this.errors_messages.push('The price is too small !');
                else if (event.target.value > 10 && this.errors_messages.indexOf('The price is too small !') !== -1) 
                    this.errors_messages.splice(this.errors_messages.indexOf('The price is too small !'), 1);
                if (event.target.value > 2000 && this.errors_messages.indexOf('The price is too big !') === -1) 
                    this.errors_messages.push('The price is too big !');
                if (event.target.value <= 2000 && this.errors_messages.indexOf('The price is too big !') !== -1) 
                    this.errors_messages.splice(this.errors_messages.indexOf('The price is too big !'), 1);               
            }
        },
        
        keyMonitorCheckEmpty(event) {
            let value = event.target.value;
            let name = event.target.name;
            let error_message = name + ' is empty !';
            if (value === "" && this.errors_messages.indexOf(error_message) === -1) {
                this.errors_messages.push(error_message);
            } else if (value !== "" && this.errors_messages.indexOf(error_message) !== -1) {
                this.errors_messages.splice(this.errors_messages.indexOf(error_message), 1);
            }
        }
    },
};
</script>

<style>
    #container-create-pet {
        text-align: left;
        margin: 4% 4%;
        border-radius: 5px;
        border: solid 1px #d50000ce;
        overflow: hidden;
        padding-top: 5px;
        width: 50%;
        margin: 0 auto;
    }

    #container-create-pet > .header-create-pet {
        border-top-left-radius: 5px;
        border-top-right-radius: 5px;
        background-color: #d5000080;
        color: #fff;
        margin-top: -20px;
        padding: 5px 0 1px 5px;
        padding-left: 20px;
    }

    #form-create-pet > h3 {
        margin: 10px;
    }

    #form-create-pet {
        padding: 10px 10px;
    }

    .form-group {
        margin: 10px;
        width: 100%;
        display: flex;
        flex-direction: column;
    }

    #pre-data {
        box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
        width: 97%;
        margin: 10px;
        border-radius: 5px;
    }

    .checkbox-group {
        display: flex;
        margin: 10px;
        flex-direction: row;
        justify-content: center;
    }

    .container-vertical-center {
        text-align: center;
        justify-content: center;
    }

    .custom-button-blue {
        background-color: #81d4fa;
        outline: none;
        border: none;
        padding: 7px;
        color: #fff;
        font-size: 16px;
        border-radius: 3px;
    }
</style>