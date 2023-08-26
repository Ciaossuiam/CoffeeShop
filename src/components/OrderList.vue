<script setup lang="ts">

</script>

<template>
  <!-- <h1>{{ msg }}</h1> -->

  <div>
    <!-- <button type=button" @click="count++">count is {{ count }}</button> -->
    <h2 class="order">訂單</h2>
    <div>
        <label for="name">品項名稱：</label>
        <input type="text" id="name">
    </div>
    <div>
        <label for="price">價格：</label>
        <input type="text" id="price">
    </div>
    <div>
        <label for="size">大小：</label>
        <select id="size">
            <option value="L">L</option>
            <option value="M">M</option>
            <option value="S">S</option>
        </select>
    </div>
    <div>
        <label for="note">備註：</label>
        <input type="text" id="note">
    </div>
    <button type="button">新增</button>
  </div>
</template>

<style lang="scss" scoped>


</style>