<template>
  <div class="main-container">
    <h1>Gerenciar pedidos:</h1>
    <Dashborad />
  </div>
</template>

<script>
import Dashboard from "../components/Dashboard.vue";
export default {
  name: "OrderView",

  components: {
    Dashboard
  }
};
</script>
