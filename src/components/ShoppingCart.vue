<script setup lang="ts">
const props = defineProps({
    data: Object
})
</script>

<template>
    <div class="shopping-cart">
        <ul>
            <li v-for="item in props.data">
                <div>品項名稱：{{ item.name }}</div>
                <div>價格：{{ item.price }}</div>
                <div>大小：{{ item.size }}</div>
                <div>備註：{{ item.note }}</div>
            </li>
        </ul>
    </div>
</template>

<style scoped>
.shopping-cart {
    width: 60%;
    color: white;
    font-weight: 700;
    & ul {
        padding: 0;
        & li {
            border-bottom: 2px dashed black;
            box-sizing: border-box;
            list-style-type: none;
            padding: 20px;
            &:last-of-type {
                border: none;
            }
        }
    }
}
</style>