<template>
    <div id="nav">

            <router-link to="/">
                <img :src="logo" :alt="alt" id="img">
            </router-link>

            <nav>
                <router-link to="/">Home</router-link> 
                <router-link to="/pedidos">Pedidos</router-link>
            </nav>

    </div>    
</template>

<script>
export default {
    name: "NavBar",
    props: ["logo", "alt"]
}
</script>

<style scoped>
#nav {
    background-color: #ffb89a;
    border-bottom: 4px solid #f8cfbe;
    padding: 5px 50px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}
img {
    width: 60px;
    height: 60px;
}
#nav a {
    color: #0c60b4;
    text-decoration: none;
    margin: 12px;
    transition: .5s;
    text-transform: uppercase;
}
#nav a:hover {
    color: #FFF;
}
</style>