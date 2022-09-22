<template>
  <div>
    <div class="main-container">
        <div class="gerencia-pedidos">
          <h1>Gerenciar pedidos</h1>
        </div>
      <Dashboard />
    </div>
  </div>
</template>

<script>
import Dashboard from '../components/Dashboard'

export default {
  name: 'Pedidos',
  components: {
    Dashboard
  }
}
</script>

<style>
#gerencia-pedidos{
  margin-top: 0px;
}
</style>
