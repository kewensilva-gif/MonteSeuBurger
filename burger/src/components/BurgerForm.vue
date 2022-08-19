<template>
  <div>
    <p>Componente de mensagem</p>
    <div>
      <form id="burger-form">
        <div class="input-container">
          <label for="nome">Nome do cliente:</label>
          <input
            type="text"
            name="nome"
            id="nome"
            v-model="nome"
            placeholder="Digite o seu nome"
          />
        </div>

        <div class="input-container">
          <label for="pao">Escolha o pão:</label>
          <select name="pao" id="pao" v-model="pao">
            <option value="" selected>Selecione o seu pão</option>
            <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{pao.tipo}}</option>
          </select>
        </div>

        <div class="input-container">
          <label for="carne">Escolha a carne:</label>
          <select name="carne" id="carne" v-model="carne">
            <option value="" selected>Selecione o tipo de carne</option>
            <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{carne.tipo}}</option>
          </select>
        </div>

        <div id="opcionais-container" class="input-container">
          <label id="opcionais-title" for="opcionais">Escolha a opcionais:</label>
          <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
            <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
            <span>{{opcional.tipo}}</span>
          </div>
        </div>

        <div class="input-container">
            <input type="submit" class="submit-btn" value="Criar meu Burger">
        </div>

      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "BurgerForm",
  data() {
    return {
      paes: null,
      carnes: null,
      opcionaisdata: null,
      nome: null,
      pao: null,
      carne: null,
      opcionais: [],
      status: 'Solicitado',
      msg: null
    };
  },
  methods: {
    async getIngredientes(){
      const req = await fetch('http://localhost:3000/ingredientes');
      const data = await req.json();

      this.paes = data.paes;
      this.carnes = data.carnes;
      this.opcionaisdata = data.opcionais;
    }
  },
  mounted() {
    this.getIngredientes()
  }
};
</script>

<style scoped>
    #burger-form {
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
        color: var(--bg-cinza-principal);
        padding: 5px 10px;
        border-left: 4px solid var(--bg-amarelo-principal);
    }

    input, select {
        padding: 5px 10px;
        width: 300px;
    }

    #opcionais-container {
        flex-direction: row;
        flex-wrap: wrap;
    }

    #opcionais-title {
        width: 100%;
    }

    #checkbox-container {
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
        background-color: var(--bg-cinza-principal);
        color: var(--bg-amarelo-principal);
        font-weight: bold;
        border: 2px solid var(--bg-cinza-principal);
        padding: 10px;
        font-size: 16px;
        position: relative;
        left: 0;
        cursor: pointer;
        transition: .5s;
    }

    .submit-btn:hover {
        background-color: transparent;
        color: var(--bg-cinza-principal);
    }
</style>