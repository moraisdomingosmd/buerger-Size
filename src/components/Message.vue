<template>
    <div class="message-container">
        <p>{{msg}}</p>
    </div>
</template>

<script>
export default {
    name: "Message",
    props: {
        msg: String
    }
}
</script>

<style scoped>
    .message-container {
        color: #0c60b4;
        background-color: #f8cfbe;
        border: 2px solid #ffb89a;
        border-radius: 5px;
        padding: 10px;
        max-width: 400px;
        margin: 30px auto;
        text-align: center;
        font-weight: bold;
    }
</style>