<template>
  <div>
    <Navbar :logo="logo_src" :alt="app_name" />
    <div>
      <router-view></router-view>
    </div>
    <Footer />
  </div>
</template>
<script>
import Navbar from './components/Navbar'
import Footer from './components/Footer'

export default {
  data: function() {
    return {
      logo_src: "/img/logo.png",
      app_name: "Renee Trajar"
    }
  },
  components: {
    Navbar,
    Footer
  }
}
</script>

<style>
  * {
    font-family: Helvetica;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .main-container {
    margin-bottom: 50px;
    margin-top:50px;
    min-height: 250px;
  }

  h1 {
    text-align: center;
    font-size: 28px;
    margin-top: 50px;
    color: #1C86A4;
    font-family: 'Cormorant';
  }

    h2 {
    margin-left:489px;
    font-size: 28px;
    margin-bottom: 30px;
    margin-top: 50px;
    color: #1C86A4;
    font-family: 'Cormorant';
  }

    h3 {
    font-size: 84px;
    margin-bottom: 96px;
    margin-left: 96px;
    margin-top: -14px;
    color: #014561;
    font-family: 'Cormorant';
  }

    h4 {
    font-size: 0.1px;
    margin-bottom: 96px;
    margin-left: 96px;
    margin-top: -14px;
    color: #014561;
    font-family: 'Cormorant';
  }
</style>
