<template>
  <div class="container mx-auto min-h-screen justify-between flex flex-col">
    <HeaderVue/>
    <Main/>
    <Footer/>
  </div>
</template>

<script>
import HeaderVue from './components/Header.vue';
import Main from './components/Main.vue'
import Footer from './components/Footer.vue'

export default {
  components : {
    HeaderVue,
    Main,
    Footer
  }
}
</script>

<style>

</style>