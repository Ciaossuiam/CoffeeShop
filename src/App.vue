<script setup lang="ts">
import { ref } from 'vue';
import OrderList from './components/OrderList.vue';
import ShoppingCart from './components/ShoppingCart.vue'

const data = ref<Array<Object>>([])
data.value = JSON.parse(localStorage.getItem('shoppingCart') as string) || []
let arr:any = data.value
const handleChildEvent = (element: object) => {
    arr = [element, ...arr]
    data.value = arr
    localStorage.setItem('shoppingCart', JSON.stringify(arr))
}
</script>

<template>
    <div class="app">
        <h2>咖啡訂單系統</h2>
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
    padding-top: 20px;
    border: 2px solid black;
    box-sizing: border-box;
    background: linear-gradient(to right, #59321D 0%, #8F6849 50%, #59321D 100%);
    & h2 {
        text-align: center;
    }
    & .order-box {
        width: 50%;
        margin-right: auto;
        margin-left: auto;
        display: flex;
        justify-content: space-between;
        padding: 20px;
    }
}
@media(max-width: 991.98px) {
    .app {
        & .order-box {
            width: 80%;
            display: block;
        }
    }
}
</style>
