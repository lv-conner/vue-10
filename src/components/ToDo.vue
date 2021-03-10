<template>
    <div>
        <h1 class="header">{{message}}</h1>
        <div v-for="item in items" :key="item">
            {{ item }}
        </div>
        <a-button type="primary">Hello</a-button>
    </div>
</template>
<script>

    export default {
        name: "Todo",
        props: {
            message: String,
            items:Array
        }
    }
</script>

<style scoped>
    .header {
        font-size: 2rem;
        font-weight: 550;
        color: red;
    }
</style>