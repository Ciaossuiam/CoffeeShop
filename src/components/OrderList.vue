<script setup lang="ts">
import { ref } from 'vue';

const emit = defineEmits();

const coffeeName = ref<string>()
const coffeePrice = ref<number>()
const coffeeSize = ref<string>()
const coffeeNote = ref<string>()
const order = ref<Object>({})

const add = () => {
    order.value = {
        name: coffeeName.value,
        price: coffeePrice.value,
        size: coffeeSize.value,
        note: coffeeNote.value
    }
    localStorage.setItem('shoppingCart', JSON.stringify(order.value))
    emit('shoppingCart', {
        name: coffeeName.value,
        price: coffeePrice.value,
        size: coffeeSize.value,
        note: coffeeNote.value
    })
}
</script>

<template>
  <!-- <h1>{{ msg }}</h1> -->

  <div class="order-list">
    <!-- <button type=button" @click="count++">count is {{ count }}</button> -->
    <div class="field">
        <label for="name">品項名稱：</label>
        <input type="text" id="name" v-model="coffeeName" autofocus>
    </div>
    <div class="field">
        <label for="price">價格：</label>
        <input type="number" id="price" v-model="coffeePrice">
    </div>
    <div class="field">
        <label for="size">大小：</label>
        <select id="size"  v-model="coffeeSize">
            <option value="L">L</option>
            <option value="M">M</option>
            <option value="S">S</option>
        </select>
    </div>
    <div class="field">
        <label for="note">備註：</label>
        <input type="text" id="note" v-model="coffeeNote" placeholder="備註">
    </div>
    <div class="order-footer">
        <button type="button" @click="add">新增</button>
    </div>
  </div>
</template>

<style scoped>
.order-list {
    font-weight: 700;
    color: white;
    & .field {
        margin: 5px;
        & input {
            height: 20px;
            border-radius: 5px;
            color: black;
        }
        & select {
            height: 20px;
            border-radius: 5px;
            color: black;
            & option {
                color: black;
            }
        }
    }
    & .order-footer {
        display: flex;
        justify-content: flex-end;
    }
    & button {
        /* background: #877865; */
        background-color: black;
        color: white;
        font-weight: 700;
    }
}
</style>