<template>
  <NavBar v-bind:logo="logo_img" v-bind:alt="alt"/>
  <RouterView />
  <Footer />
</template>

<script>
import NavBar from "./components/NavBar.vue";
import Footer from "./components/Footer.vue";

export default {
  components: {
    NavBar,
    Footer,
  },
  data() {
    return {
      logo_img: "/img/Icon_burguer.png",
      app_name: "Logo do sistema",
    };
  },
};
</script>

<style>
  * {
    font-family: Helvetica;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }
  .main-container {
    margin: 50px;
    min-height: 250px;
  }
  h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
  }
</style>
