<template>
  <Message :msg="msg" v-show="msg" />
  <div>
    <form id="burger-form" method="POST" @submit="createBurger">
      <div class="input-container">
        <label for="nome">Nome do cliente:</label>
        <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome">
      </div>
      <div class="input-container">
        <label for="pao">Escolha o pão:</label>
        <select name="pao" id="pao" v-model="pao">
          <option value="">Selecione o seu pão</option>
          <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
        </select>
      </div>
      <div class="input-container">
        <label for="carne">Escolha a carne do seu Burger:</label>
        <select name="carne" id="carne" v-model="carne">
          <option value="">Selecione o tipo de carne</option>
          <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
        </select>
      </div>
      <div id="opcionais-container" class="input-container">
        <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
        <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
          <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
          <span>{{ opcional.tipo }}</span>
        </div>
      </div>
      <div class="input-container">
        <input class="submit-btn" type="submit" value="Criar meu Burger!">
      </div>
    </form>
  </div>
</template>

<script>
import Message from './Message.vue'

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
      status: "Solicitado",
      msg: null
    }
  },
  methods: {
    async getIngredientes() {
      const req = await fetch('http://localhost:3000/ingredientes')
      const data = await req.json()

      this.paes = data.paes
      this.carnes = data.carnes
      this.opcionaisdata = data.opcionais
    },
    async createBurger(e) {

      e.preventDefault()

      const data = {
        nome: this.nome,
        carne: this.carne,
        pao: this.pao,
        opcionais: Array.from(this.opcionais),
        status: "Solicitado"
      }

      const dataJson = JSON.stringify(data)    

      const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: { "Content-Type" : "application/json" },
        body: dataJson
      });

      const res = await req.json()

      console.log(res)

      this.msg = "Pedido realizado com sucesso!"

      // clear message
      setTimeout(() => this.msg = "", 3000)

      // limpar campos
      this.nome = ""
      this.carne = ""
      this.pao = ""
      this.opcionais = []
      
    }
  },
  mounted () {
    this.getIngredientes()
  },
  components: {
    Message
  }
}
</script>

<style scoped>
#burger-form {
  max-width: 400px;
  margin: 0 auto;
  padding-top: 1rem;
}

.input-container {
  margin-bottom: 20px;
}

label {
  font-weight: bold;
  margin-bottom: 5px;
  color: #333;
}

input,
select {
  padding: 10px;
  width: 100%;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

#opcionais-container {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 20px;
}

#opcionais-title {
  width: 100%;
  font-weight: bold;
  margin-bottom: 10px;
}

.checkbox-container {
  display: flex;
  align-items: center;
  width: 50%;
  margin-bottom: 10px;
}

.checkbox-container span {
  margin-left: 6px;
  font-weight: normal;
  color: #444;
}

.submit-btn {
  background-color: #fcba03;
  color: #333;
  font-weight: bold;
  border: none;
  padding: 12px 20px;
  font-size: 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s, color 0.3s;
}

.submit-btn:hover {
  background-color: #333;
  color: #fcba03;
}


</style>