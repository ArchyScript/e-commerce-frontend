<template>
  <v-footer width="100%">
    <ContactUs />
    <!-- <Test /> -->
  </v-footer>
</template>

<script>
import ContactUs from "./ContactUs.vue";
// import Test from "./Test.vue";
export default {
  name: "Footer",

  data: () => ({
    icons: ["mdi-facebook", "mdi-twitter", "mdi-linkedin", "mdi-instagram"],
  }),

  components: {
    ContactUs,
    // Test,
  },
};
</script>