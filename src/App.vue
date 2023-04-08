<template>
  <Navbar :logo="logoSrc" :alt="appName"/>
  <router-view/>
  <Footer />
</template>

<script>
import Navbar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";

export default {
  components: {
    Navbar,
    Footer
  },
  data() {
    return {
      logoSrc: "/img/logo.png",
      appName: "Make your Veg Burguer"
    }
  }
}
</script>

<style>
  * {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: Helvetica, sans-serif;
  }

  .mainContainer {
    margin: 3.2rem;
    min-height: 15.6rem;
  }

  h1 {
    text-align: center;
    font-size: 2.6rem;
    margin-bottom: 1.8rem;
    color: #222;
  }
</style>
