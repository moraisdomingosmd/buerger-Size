<template>
  
  <NavBar :logo="logo_img" :alt="alt_txt"/>
  <router-view/>
  <Footer />
</template>

<script>
import NavBar from './components/navBar.vue'
import Footer from './components/Footer.vue'

export default {
  components: {
    NavBar,
    Footer
  },
  data() {
    return {
      logo_img: "/img/buerger.png",
      alt_txt: "Buerger Zone"
    }
  }
}
</script>

<style>
*{
    padding: 0;
    margin: 0;
    vertical-align: baseline;
    list-style: square;
    box-sizing: border-box;
    font-family: Helvetica;
}
body {
  background-color: #f1f1f1;
}
.main-container {
  margin: 50px;
  min-height: 250px;
}
h1 {
  font-size: 42px;
  margin-bottom: 30px;
  color: #222;
  text-align: center;
}
</style>
