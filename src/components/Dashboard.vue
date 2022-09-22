<template>
  <div id="conjunto-table" v-if="conjuntos">
    <div>
      <div id="conjunto-table-heading">
        <div class="order-id">#:</div>
        <div>Cliente:</div>
        <div>Blusa:</div>
        <div>Sobre a blusa:</div>
        <div>Opcionais:</div>
        <div>Ações:</div>
      </div>
    </div>
    <div id="conjunto-table-rows">
      <div class="conjunto-table-row" v-for="conjunto in conjuntos" :key="conjunto.id">
        <div class="order-number">{{ conjunto.id }}</div>
        <div>{{ conjunto.nome }}</div>
        <div>{{ conjunto.blusa }}</div>
        <div>{{ conjunto.sobreblusa }}</div>
        <div>
          <ul v-for="(opcional, index) in conjunto.opcionais" :key="index">
            <li>{{ opcional }}</li>
          </ul>
        </div>
        <div>
          <select name="status" class="status" @change="updateConjunto($event, conjunto.id)">
            <option :value="s.tipo" v-for="s in status" :key="s.id" :selected="conjunto.status == s.tipo">
              {{ s.tipo }}
            </option>
          </select>
          <button class="delete-btn" @click="deleteConjunto(conjunto.id)">Cancelar</button>
        </div>
      </div>
    </div>
  </div>
  <div v-else>
    <h2>Não há pedidos no momento!</h2>
  </div>
</template>
<script>
  export default {
    name: "Dashboard",
    data() {
      return {
        conjuntos: null,
        conjunto_id: null,
        status: []
      }
    },
    methods: {
      async getPedidos() {
        const req = await fetch('http://localhost:3000/conjuntos')

        const data = await req.json()

        this.conjuntos = data

        // Resgata os status de pedidos
        this.getStatus()

      },
      async getStatus() {

        const req = await fetch('http://localhost:3000/status')

        const data = await req.json()

        this.status = data

      },
      async deleteConjunto(id) {

        const req = await fetch(`http://localhost:3000/conjuntos/${id}`, {
          method: "DELETE"
        });

        const res = await req.json()

        this.getPedidos()

      },
      async updateConjunto(event, id) {

        const option = event.target.value;

        const dataJson = JSON.stringify({status: option});

        const req = await fetch(`http://localhost:3000/conjuntos/${id}`, {
          method: "PATCH",
          headers: { "Content-Type" : "application/json" },
          body: dataJson
        });

        const res = await req.json()

        console.log(res)

      }
    },
    mounted () {
    this.getPedidos()
    }
  }
</script>

<style scoped>
  #conjunto-table {
    max-width: 1200px;
    margin: 0 auto;
  }

  #conjunto-table-heading,
  #conjunto-table-rows,
  .conjunto-table-row {
    display: flex;
    flex-wrap: wrap;
  }

  #conjunto-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
  }

  .conjunto-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
  }

  #conjunto-table-heading div,
  .conjunto-table-row div {
    width: 19%;
  }

  #conjunto-table-heading .order-id,
  .conjunto-table-row .order-number {
    width: 5%;
  }

  select {
    padding: 12px 6px;
    margin-right: 12px;
    margin-bottom: 10px;
    border-radius: 4px;
  }

  .delete-btn {
    background-color: #014561;
    color:#FFF;
    font-weight: bold;
    border: 2px solid #014561;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
    border-radius:4px;
  }
  
  .delete-btn:hover {
    background-color: #00628b;
    color: #FFF;

  }
  
</style>