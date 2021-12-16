<template>
  <v-app class="grey">
    <Layout />

    <v-main class="mx-4 my-3 dark">
      <!-- Other routes -->
      <router-view />

      <Footer />
    </v-main>
  </v-app>
</template> 

<script lang="js">
// import Vue from "vue";
import Layout from "@/components/Layout.vue";
import Footer from "@/components/Footer/Main.vue";

export default {
  name: "App",

  components: {
    Layout,
    Footer,
  },
  data: () => ({
    //
  }),
};
</script>