<script setup lang="ts">
import { ref } from 'vue';

const editingCoffeeName = ref<string>()
const editingCoffeePrice = ref<number>()
const editingCoffeeSize = ref<string>()
const editingCoffeeCups = ref<number>()
const editingCoffeeNote = ref<string>()

const props = defineProps({
    data: Object
})
const edit = (e: any) => {
    editingCoffeeName.value = e.name
    editingCoffeePrice.value = e.price
    editingCoffeeSize.value = e.size
    editingCoffeeCups.value = e.cups
    editingCoffeeNote.value = e.note
    e.isEditing = true
}
const save = (e: any) => {
    props.data?.splice(props.data?.indexOf(e), 1, {
        name: editingCoffeeName.value,
        price: editingCoffeePrice.value,
        size: editingCoffeeSize.value,
        cups: editingCoffeeCups.value,
        note: editingCoffeeNote.value,
    })
    e.isEditing = false
    localStorage.setItem('shoppingCart', JSON.stringify(props.data))
}
const remove = (e: any) => {
    props.data?.splice(props.data?.indexOf(e), 1)
    localStorage.setItem('shoppingCart', JSON.stringify(props.data))
}
</script>

<template>
    <div class="shopping-cart">
        <ul>
            <li v-for="item in props.data">
                <div class="editing-list" v-if="item.isEditing">
                    <div>品項名稱：
                        <input type="text" v-model="editingCoffeeName">
                    </div>
                    <div>價格：
                        <input type="number" min="0" v-model="editingCoffeePrice">
                    </div>
                    <div>大小：
                        <select v-model="editingCoffeeSize">
                            <option value="L">L</option>
                            <option value="M">M</option>
                            <option value="S">S</option>
                        </select>
                    </div>
                    <div>杯數：
                        <input type="number" min="0" v-model="editingCoffeeCups">
                    </div>
                    <div>備註：
                        <input type="text" v-model="editingCoffeeNote">
                    </div>
                </div>
                <div v-else>
                    <div>品項名稱：{{ item.name }}</div>
                    <div>價格：{{ item.price }} ( TWD )</div>
                    <div>大小：{{ item.size }}</div>
                    <div>杯數：{{ item.cups }} ( 杯 )</div>
                    <div v-if="item.note">備註：{{ item.note }}</div>
                    <div v-else>備註：無</div>
                </div>
                <div>
                    <div class="action-box">
                        <button class="edit" v-if="item.isEditing" @click="save(item)">保存</button>
                        <button class="edit" v-else @click="edit(item)">編輯</button>
                    </div>
                    <div class="action-box">
                        <button class="remove" @click="remove(item)">刪除</button>
                    </div>
                </div>
            </li>
        </ul>
    </div>
</template>

<style scoped>
.shopping-cart {
    width: 60%;
    color: white;
    font-weight: 700;
    margin-left: 50px;
    & ul {
        padding: 0;
        & li {
            border-bottom: 2px dashed black;
            box-sizing: border-box;
            list-style-type: none;
            padding: 20px;
            display: flex;
            justify-content: space-between;
            &:last-of-type {
                border: none;
            }
            & .editing-list {
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
            & .action-box {
                margin: 5px;
                & .edit {
                    background: #FFC107;
                    font-weight: 700;
                }
                & .remove {
                    background: red;
                    font-weight: 700;
                }
            }
        }
    }
}
@media(max-width: 991.98px) {
    .shopping-cart {
        width: 80%;
    }
}
</style>