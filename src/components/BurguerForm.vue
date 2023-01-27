<template>
  <div>
    <p>Componete de mensagem</p>
  </div>
  <div>
    <form id="burguer-form">
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
          <option value="Integral">Integral</option>
        </select>
      </div>
      <div class="input-container">
        <label for="meat">Escolha a carne do seu burguer:</label>
        <select form="meat" v-model="meat">
          <option value="">Selecione o tipo da carne</option>
          <option value="picanha">Picanha</option>
        </select>
      </div>
      <div id="options-container" class="input-container">
        <label id="options-title" for="options">Selecione os opcionais:</label>
        <div class="checkbox-container">
            <input type="checkbox" name="options" v-model="options" value="salami">
            <span>Salame</span>
        </div>
      </div>
      <div class="input-container">
        <input type="submit" class="submit-btn" value="Criar meu burguer">
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "BurguerForm",
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
    color: #222;;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
  }
  input, select {
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
    color:#fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }
  .submit-btn:hover {
    background-color: transparent;
    color: #222;
  }
</style>