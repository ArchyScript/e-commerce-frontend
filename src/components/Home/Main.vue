<template>
  <div>
    <Home />

    <v-divider></v-divider>

    <Categories />

    <v-divider></v-divider>

    <!-- 
    <Cart />
    <Basket /> 

    <v-divider></v-divider> -->

    <Contact />
  </div>
</template>

<script>
import Home from './Home.vue'
// import Basket from './Basket.vue'
import Categories from './Categories.vue'
// import Adsense from "./Adsense.vue";
import Contact from './Contact.vue'
// import Cart from "./Cart.vue";

export default {
  data: () => ({}),
  components: {
    Home,
    // Basket,
    Categories,
    // Adsense,
    Contact,
    // Cart,
  },
}
</script>
