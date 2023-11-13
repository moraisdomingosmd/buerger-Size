<template>
    <Painel />
  <div class="main-container">
    <h1>Monte o seu pedido:</h1>
    <SizeForm />
  </div>
</template>

<script>
  import Painel from '../components/Painel.vue'
  import SizeForm from '../components/SizeForm.vue' 

  export default {
    name: "Home",
    components: {
     Painel,
     SizeForm
    }
  }
</script>

