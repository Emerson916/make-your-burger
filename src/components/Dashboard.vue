<template>
  <div id="burger-table" v-if="burguers">
    <div>
      <div id="burger-table-heading">
        <div class="order-id">#:</div>
        <div>Cliente:</div>
        <div>Pão:</div>
        <div>Carne:</div>
        <div>Opcionais:</div>
        <div>Ações:</div>
      </div>
    </div>
    <div id="burger-table-rows">
      <div
        class="burger-table-row"
        v-for="burguer in burguers"
        :key="burguer.id"
      >
        <div class="order-number">{{ burguer.id }}</div>
        <div>{{ burguer.nome }}</div>
        <div>{{ burguer.pao }}</div>
        <div>{{ burguer.carne }}</div>
        <div>
          <ul v-for="(opcional, index) in burguer.opcionais" :key="index">
            <li>{{ opcional }}</li>
          </ul>
        </div>
        <div>
          <select name="status" class="status">
            <option>teste</option>
          </select>
          <button class="delete-btn" @click="deleteBurger(burguer.id)">
            Cancelar
          </button>
        </div>
      </div>
    </div>
  </div>
  <div v-else>
    <h2>Não há pedidos no momento!</h2>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Dashboard",
  data() {
    return {
      burguers: null,
      burguers_id: null,
      status: [],
    };
  },

  methods: {
    async getPedidos() {
      const req = await axios.get("http://localhost:3000/burguers");

      this.burguers = req.data;
    },
  },

  mounted() {
    this.getPedidos();
  },
};
</script>

<style scoped>
#burger-table {
  max-width: 1200px;
  margin: 0 auto;
}
#burger-table-heading,
#burger-table-rows,
.burger-table-row {
  display: flex;
  flex-wrap: wrap;
}
#burger-table-heading {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid #333;
}
.burger-table-row {
  width: 100%;
  padding: 12px;
  border-bottom: 1px solid #ccc;
}
#burger-table-heading div,
.burger-table-row div {
  width: 19%;
}
#burger-table-heading .order-id,
.burger-table-row .order-number {
  width: 5%;
}
select {
  padding: 12px 6px;
  margin-right: 12px;
}
.delete-btn {
  background-color: #222;
  color: #fcba03;
  font-weight: bold;
  border: 2px solid #222;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: 0.5s;
}

.delete-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>
