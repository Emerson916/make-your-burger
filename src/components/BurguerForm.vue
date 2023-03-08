<template>
  <div>
    <p>Componete de mensagem</p>
  </div>
  <div>
    <form id="burguer-form" @submit="createBurguer">
      <div class="input-container">
        <label for="name">Nome do cliente:</label>
        <input
          type="text"
          id="name"
          name="name"
          v-model="name"
          placeholder="Digite o seu nome"
        />
      </div>
      <div class="input-container">
        <label for="bread">Escolha o pão:</label>
        <select form="bread" v-model="bread">
          <option value="">Selecione seu pão</option>
          <option
            v-for="bread in breadsDate"
            v-bind:key="bread.id"
            v-bind:value="bread.tipo"
          >
            {{ bread.tipo }}
          </option>
        </select>
      </div>
      <div class="input-container">
        <label for="meat">Escolha a carne do seu burguer:</label>
        <select form="meat" v-model="meat">
          <option value="">Selecione o tipo da carne</option>
          <option
            v-for="meat in meatData"
            v-bind:key="meat.id"
            v-bind:value="meat.tipo"
          >
            {{ meat.tipo }}
          </option>
        </select>
      </div>
      <div id="options-container" class="input-container">
        <label id="options-title" for="options">Selecione os opcionais:</label>
        <div
          class="checkbox-container"
          v-for="optionsItens in optionsData"
          v-bind:key="optionsItens.id"
        >
          <input
            type="checkbox"
            name="options"
            v-model="options"
            v-bind:value="optionsItens.tipo"
          />
          <span>{{ optionsItens.tipo }}</span>
        </div>
      </div>
      <div class="input-container">
        <input type="submit" class="submit-btn" value="Criar meu burguer" />
      </div>
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "BurguerForm",

  data() {
    return {
      //estado que guarda os valores que VEM do servidor
      breadsDate: null,
      meatData: null,
      optionsData: null,

      //estado que guarda os valores que VÃO para o servidor
      name: null,
      bread: null,
      meat: null,
      options: [],
      status: "Solicitado",
      msg: null,
    };
  },
  methods: {
    async getIngredients() {
      await axios.get("http://localhost:3000/ingredientes").then((response) => {
        (this.breadsDate = response.data.breadsDate),
          (this.meatData = response.data.meatData),
          (this.optionsData = response.data.optionsData);
      });
    },

    async createBurguer(e) {
      e.preventDefault();
      const data = {
        nome: this.name,
        carne: this.meat,
        pao: this.bread,
        opcionais: Array.from(this.options),
        status: "Solicitado",
      };

      const dataJson = JSON.stringify(data);

      const req = await axios.post("http://localhost:3000/burguers", dataJson, {
        headers: { "Content-Type": "application/json" },
      });

      if (req) {
        this.name = "",
        this.meat = "",
        this.bread = "",
        this.options = ""
      }

    },
  },
  mounted() {
    this.getIngredients();
  },
};
</script>

<style scoped>
#burguer-form {
  max-width: 400px;
  margin: 0 auto;
}
.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}
label {
  font-weight: bold;
  margin-bottom: 15px;
  color: #222;
  padding: 5px 10px;
  border-left: 4px solid #fcba03;
}
input,
select {
  border: 1px solid #222;
  outline-style: none;
  border-radius: 5px;
  padding: 5px 10px;
  width: 300px;
}
#options-container {
  flex-direction: row;
  flex-wrap: wrap;
}
#options-title {
  width: 100%;
}
.checkbox-container {
  display: flex;
  align-items: flex-start;
  width: 50%;
  margin-bottom: 20px;
}
.checkbox-container span,
.checkbox-container input {
  width: auto;
}
.checkbox-container span {
  margin-left: 6px;
  font-weight: bold;
}
.submit-btn {
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
.submit-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>
