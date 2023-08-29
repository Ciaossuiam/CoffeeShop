<script setup lang="ts">
import { ref } from 'vue';

const emit = defineEmits();
let uuid:string;
const coffeeName = ref<string>()
const coffeePrice = ref<number>()
const coffeeSize = ref<string>()
const coffeeCups = ref<number>(1)
const coffeeNote = ref<string>()

const add = () => {
    if(coffeeName.value && coffeePrice.value && coffeeSize.value  && coffeeCups.value) { // 當除了 note 以外的輸入框都被寫入
        // uuid 製作
        uuid = Math.floor((1 + Math.random()) * 0x10000).toString(16).substring(1)
        
        // 資料回傳父層
        emit('shoppingCart', {
            id: uuid,
            name: coffeeName.value,
            price: coffeePrice.value,
            size: coffeeSize.value,
            cups: coffeeCups.value,
            note: coffeeNote.value,
            isEditing: false
        })
    } else {
        alert('未填寫完整!')
    }

}
</script>

<template>
  <!-- <h1>{{ msg }}</h1> -->

  <div class="order-list">
    <!-- <button type=button" @click="count++">count is {{ count }}</button> -->
    <div class="field">
        <label for="name">品項名稱*：</label>
        <input type="text" id="name" v-model="coffeeName" autofocus>
    </div>
    <div class="field">
        <label for="price">價格*：</label>
        <input type="number" id="price" min="0" v-model="coffeePrice">
    </div>
    <div class="field">
        <label for="size">大小*：</label>
        <select id="size"  v-model="coffeeSize">
            <option value="L">L</option>
            <option value="M">M</option>
            <option value="S">S</option>
        </select>
    </div>
    <div class="field">
        <label for="cups">杯數*：</label>
        <input type="number" id="cups" min="0" v-model="coffeeCups">
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
        & label {
            display: flex;
            height: 20px;
        }
        & input {
            height: 20px;
            border-radius: 5px;
            color: black;
        }
        & select {
            height: 20px;
            border: 2px inset black;
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
        background-color: black;
        color: white;
        font-weight: 700;
    }
}
@media(max-width: 991.98px) {
    .order-list {
        width: 50%;
        margin-right: auto;
        margin-left: auto;
    }
}
</style>