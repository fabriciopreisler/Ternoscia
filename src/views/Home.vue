<template>
  <div>
    <div class="main-container">
      <Banner></Banner>
      <Banner2></Banner2>
      <Banner3></Banner3>
      <Banner7></Banner7>
      <Banner4></Banner4>
      <Banner5></Banner5>
      <Banner6></Banner6>
      <h2>Contato</h2>
      <Contato></Contato>

    </div>
  </div>
</template>

<script>
import Contato from '../components/Contato'
import Banner from "../components/Banner.vue"
import Banner1 from '../components/Banner.vue'
import Banner2 from '../components/Banner2.vue'
import Banner3 from '../components/Banner3.vue'
import Banner4 from '../components/Banner4.vue'
import Banner5 from '../components/Banner5.vue'
import Banner6 from '../components/Carrosel/Banner6.vue'
import Banner7 from '../components/Banner7.vue'





export default {
  name: 'Home',
  components: {
    Contato,
    Banner,
    Banner1,
    Banner2,
    Banner3,
    Banner4,
    Banner5,
    Banner6,
    Banner7,
}

}
</script>