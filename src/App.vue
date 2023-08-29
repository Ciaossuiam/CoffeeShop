<script setup lang="ts">
import { ref } from 'vue';
import OrderList from './components/OrderList.vue';
import ShoppingCart from './components/ShoppingCart.vue'

const data = ref<Array<Object>>([])
let arr:any = []
const handleChildEvent = (element: object) => {
    arr = [element, ...arr]
    data.value = arr
}
</script>

<template>
    <div class="app">
        <div class="order-box">
            <OrderList @shoppingCart="handleChildEvent" />
            <ShoppingCart :data="data" />
        </div>
    </div>
</template>

<style scoped>
.app {
    width: 100%;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    padding-top: 20px;
    border: 2px solid black;
    box-sizing: border-box;
    background: linear-gradient(to right, #59321D 0%, #8F6849 50%, #59321D 100%);
    & .order-box {
        width: 50%;
        display: flex;
        justify-content: space-between;
        padding: 20px;
    }
}
</style>
