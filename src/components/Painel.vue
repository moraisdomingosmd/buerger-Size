<template>
    <div id="main-banner">
        <h1>Buerger Size</h1>
    </div>
</template>

<script>
export default {
    name: "Banner",
}
</script>

<style scoped>
#main-banner {
    background-image: url('/public/img/buerzone.jpg');    
    background-size: contain;
    height: 400px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
}
h1 {
    font-size: 60px;
    color: #0c60b4;
    text-align: center;
    background-color: #ffb89a;
    padding: 20px 40px;
    border-radius: 20px;
}
</style>