<template>
    <div id="header">
        <h1>Vue.Js Pet Depot</h1>
        <p>{{ lengthCart }} <i class="fas fa-shopping-cart"></i> Checkout</p>
    </div>
</template>

<script>
export default {
    name: 'Header',
    props: ['lengthCart'],
}
</script>

<style>
    #header {
        position: absolute;
        top: 0;
        background-color: rgba(143, 140, 140, 0.513);
        width: 100%;
        margin-left: -10px;
        padding-left: 15px;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    #header > p {
        border: solid 1px black;
        padding: 5px;
        border-radius: 3px;
    }

    #header > p, h1 {
        margin: 1% 3%;
    }
</style>
