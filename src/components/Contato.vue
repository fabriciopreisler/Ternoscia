<template>
  <Message :msg="msg" v-show="msg" />
  <div>
    <form id="Contato" method="POST" @submit="createConjunto">
      <div class="input-container">
        <label for="nome">Nome</label>
        <input type="text" id="nome" name="nome" v-model="nome">
      </div>

            <div class="input-container">
        <label for="nome">E-mail</label>
        <input type="text" id="nome" name="email" v-model="email">
      </div>

            <div class="input-container">
        <label for="mensagem">Mensagem</label>
        <input type="text" id="mensagem" name="mensagem" v-model="mensagem" placeholder="Digite sua mensagem">
      </div>

      <div class="input-container">
        <label for="blusa">Escolha sua blusa:</label>
        <select name="blusa" id="blusa" v-model="blusa">
          <option value="">Selecione</option>
          <option v-for="blusa in blusas" :key="blusa.id" :value="blusa.tipo">{{ blusa.tipo }}</option>
        </select>
      </div>
      <div class="input-container">
        <label for="sobreblusa">preferencia do que vestir?</label>
        <select name="sobreblusa" id="sobreblusa" v-model="sobreblusa">
          <option value="">Selecione</option>
          <option v-for="sobreblusa in sobreblusas" :key="sobreblusa.id" :value="sobreblusa.tipo">{{ sobreblusa.tipo }}</option>
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
        <input class="submit-btn" type="submit" value="Enviar mensagem">
      </div>
    </form>
            <br>
              <div class="tel">
                <label for="Telefone">TELEFONES</label>
                <p class="texts">+55 (11)3088-0757</p>
              </div>
              <div class="emails">
                <label for="email">E-MAIL</label>
                <p class="texts">renee@reneetrajar.com.br</p>
              </div>
  </div>
</template>

<script>
import Message from './Message'

export default {
  name: "Contato",
  data() {
    return {
      blusas: null,
      sobreblusas: null,
      opcionaisdata: null,
      nome: null,
      blusa: null,
      sobreblusa: null,
      opcionais: [],
      status: "Solicitado",
      msg: null
    }
  },
  methods: {
    async getRoupas() {
      const req = await fetch('http://localhost:3000/roupas')
      const data = await req.json()

      this.blusas = data.blusas
      this.sobreblusas = data.sobreblusas
      this.opcionaisdata = data.opcionais
    },
    async createConjunto(e) {

      e.preventDefault()

      const data = {
        nome: this.nome,
        sobreblusa: this.sobreblusa,
        blusa: this.blusa,
        opcionais: Array.from(this.opcionais),
        status: "Solicitado"
      }

      const dataJson = JSON.stringify(data)    

      const req = await fetch("http://localhost:3000/conjuntos", {
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
      this.sobreblusa = ""
      this.blusa = ""
      this.opcionais = []
      
    }
  },
  mounted () {
    this.getRoupas()
  },
  components: {
    Message
  }
}
</script>

<style scoped>
  #Contato {
    max-width: 400px;
    margin: 0 auto;
  }

  .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }

  label {
    font-weight: medium;
    margin-bottom: 15px;
    color: #1C86A4;
    font-family:Cormorant;
  }

  input#mensagem {
      width: 300px;
      height: 150px;
      word-wrap: break-word;
      overflow: hidden;
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
    color:#014561;
  }

  .submit-btn {
    background-color: #014561;
    border-radius:4px;
    color:#FFF;
    border: 1px solid #014561;
    padding: 10px;
    font-size: 16px;
    font-family: Lato;
    cursor: pointer;
    transition: .5s;
  }

  .submit-btn:hover {
    background-color: transparent;
    color: #FFF;
     background-color:#00628b;
  }

.placeholder {
  overflow: hidden;
}

select[data-v-aae30ed8] {
    padding: 12px 6px;
    margin-right: 12px;
    margin-bottom: 10px;
    border-radius: 4px;
}

.tel{
  margin-left:30px;
  margin-top: -764px;
}
.emails{
  margin-left:30px;
}

.texts{
    font-weight: bold;
    color: #014561;
}


</style>

