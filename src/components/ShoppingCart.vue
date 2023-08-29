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
                <div>
                    <div>
                        <label for="name">品項名稱：{{ item.name }}</label>
                        <input type="text" id="name" v-if="item.isEditing" v-model="editingCoffeeName">
                    </div>
                    <div>
                        <label for="price">價格：{{ item.price }} ( TWD )</label>
                        <input type="number" id="price" min="0" v-if="item.isEditing" v-model="editingCoffeePrice">
                    </div>
                    <div>
                        <label for="size">大小：{{ item.size }}</label>
                        <select v-if="item.isEditing" id="size" v-model="editingCoffeeSize">
                            <option value="L">L</option>
                            <option value="M">M</option>
                            <option value="S">S</option>
                        </select>
                    </div>
                    <div>
                        <label for="cups">杯數：{{ item.cups }} ( 杯 )</label>
                        <input type="number" id="cups" min="0" v-if="item.isEditing" v-model="editingCoffeeCups">
                    </div>
                    <div v-if="item.note">
                        <label for="note">備註：{{ item.note }}</label>
                        <input type="text" id="note" v-if="item.isEditing" v-model="editingCoffeeNote">
                    </div>
                    <div v-else>
                        <label for="note">備註：無</label>
                        <input type="text" id="note" v-if="item.isEditing" v-model="editingCoffeeNote">
                    </div>
                </div>
                <div>
                    <div class="action-box">
                        <button class="save" v-if="item.isEditing" @click="save(item)">保存</button>
                        <button class="edit" v-else @click="edit(item)">編輯</button>
                    </div>
                    <div class="action-box">
                        <button class="remove" v-if="!item.isEditing" @click="remove(item)">刪除</button>
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
            & label {
                height: 30px;
            }
            & input {
                height: 20px;
                border-radius: 5px;
                color: black;
                margin-left: 5px;
            }
            & select {
                height: 20px;
                border: 2px inset black;
                border-radius: 5px;
                color: black;
                margin-left: 5px;
                & option {
                    color: black;
                }
            }
            & .action-box {
                margin: 5px;
                & .save {
                    background: #28A745;
                    font-weight: 700;
                }
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