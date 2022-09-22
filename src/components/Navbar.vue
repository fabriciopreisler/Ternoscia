<template>
  <div>
    <div id="nav">
      <router-link id="logo-url" to="/">
        <img id="logo" :src="logo" :alt="alt">
      </router-link>
      <router-link to="/">EMPRESA</router-link>
      <router-link to="/pedidos">CAMISARIA</router-link>
      <li class="nav-item">
        <a class="nav-link" href="#">ALFAIATARIA</a>
      </li>
            <li class="nav-item">
        <a class="nav-link" href="#">DEPOIMENTOS</a>
      </li>
            <li class="nav-item">
        <a class="nav-link" href="#">CONTATOS</a>
      </li>
    </div>
  </div>
</template>

<script>

export default {
  name: "Navbar",
  props: ["logo", "alt"]
}
</script>

<style scoped>
  #nav {
    background-color: #222;
    border-bottom: 4px solid #222;
    padding: 2px 22px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    position: fixed;
    margin-top: -51px;
    width: 100%;
  }

  #nav #logo-url {
    margin: auto;
    margin-left: 0;
  }

  #logo {
    width: 40px;
    height: 40px;
  }

  #nav a {
    font-family: 'Lato';
    color: #949494;
    text-decoration: none;
    margin: 12px;
    transition: .5s;
  }

  #nav a:hover {
    color: #1C86A4;
  }
</style>