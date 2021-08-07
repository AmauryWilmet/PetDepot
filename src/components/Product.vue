<template>
    <div id="product">
        <div class="row">
            <div class="col">
                <img class="product-image" :src="image">
            </div>
            <div class="col">
                <h3>{{ title }}</h3>
                <p>{{ description }}</p>
                <p>{{ price }}</p>
                <div class="row">
                    <button v-if="isPreview === false" @click="addToCart" class="custom-button-red">Add to cart</button>
                    <div id="container-stars" v-for="i in 5" :key="i">
                        <Star v-if="i <= idStarSelected" :selected="true" :starId="i" @mouseEnterStar="selectStar" @clickStar="clickStar" />
                        <Star v-else :selected="false" :starId="i" @mouseEnterStar="selectStar" @clickStar="clickStar" />
                    </div>     
                </div>       
            </div>
        </div>
    </div>
</template>

<script>
import Star from "./Star.vue";

export default {
    name: 'Product',
    components: {
        Star,
    },
    data() {
        return {
            selected: false,
            idStarSelected: -1,
            idStarClicked: -1,
        };
    },
    props: ['title', 'description', 'image', 'price', 'addToCart', 'isPreview', 'stars'],
    methods: {
        addToCart() {
            this.addToCart();
        },
        selectStar(starId) {
            this.idStarSelected = starId;
        },
        clickStar(starId) {
            this.idStarClicked = starId;
            this.$emit('clickStar', this.idStarClicked);
        }
    },
    computed: {
        price() {
            return this.price + "€";
        }
    },
};
</script>

<style>
    .product-image {
        width: 200px;
        height: 200px;
    }

    .row {
        display: flex;
        flex-direction: row;
    }    

    .col {
        align-self: center;
        padding: 10px;
    }

    .custom-button-red {
        background-color: #d50000;
        outline: none;
        border: none;
        padding: 7px;
        color: #fff;
        font-size: 16px;
        border-radius: 3px;
        margin-right: 10px;;
    }

    #container-stars {
        padding: 2px;
    }
</style>