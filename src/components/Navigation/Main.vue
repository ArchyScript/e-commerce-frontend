<template >
  <nav>
    <!-- <v-system-bar color="deep-purple darken-3"></v-system-bar> -->
    <v-app-bar app flat color="grey lighten-4">
      <!-- Topbar -->
      <v-toolbar app flat class="grey lighten-4">
        <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

        <v-toolbar-title>
          <span class=""> ArchyStores </span>
        </v-toolbar-title>
      </v-toolbar>
      <v-spacer></v-spacer>

      <!-- Profile Links -->
      <!-- <template>
        <div
          class="d-flex justify-center align-center mr-2"
          style="user-select: none"
        >
          <v-img
            alt="Profile Picture"
            class="mx-2 rounded-circle"
            contain
            transition="scale-transition"
            width="30"
            outlined
            src="@/assets/logo.png"
          />

          <div class="text-center">
            <v-menu offset-y>
              <template v-slot:activator="{ on, attrs }">
                <span
                  color="primary"
                  dark
                  v-bind="attrs"
                  v-on="on"
                  style="user-select: none"
                >
                  <span> Manage Account </span>

                  <v-icon right> mdi-checkbox-marked-circle </v-icon>
                </span>
              </template>

              <v-list>
                <v-list-item>
                  <v-img
                    alt="Profile.nickname"
                    class="mx-2 rounded-circle"
                    contain
                    transition="scale-transition"
                    width="20"
                    outlined
                    src="@/assets/logo.png"
                  />

                  <v-list-item-title @click="goToProfile">
                    Profile
                  </v-list-item-title>
                </v-list-item>

                <v-list-item>
                  <v-img
                    class="mx-2 rounded-circle"
                    contain
                    transition="scale-transition"
                    width="20"
                    outlined
                    src="@/assets/logo.png"
                  />

                  <v-list-item-title @click="uploadPicture">
                    Upload
                  </v-list-item-title>
                </v-list-item>

                <v-list-item>
                  <v-img
                    class="mx-2 rounded-circle"
                    contain
                    transition="scale-transition"
                    width="20"
                    outlined
                    src="@/assets/logo.png"
                  />

                  <v-list-item-title @click="settings">
                    Settings
                  </v-list-item-title>
                </v-list-item>

                <v-list-item>
                  <v-img
                    class="mx-2 rounded-circle"
                    contain
                    transition="scale-transition"
                    width="20"
                    outlined
                    src="@/assets/logo.png"
                  />

                  <v-list-item-title @click="logout">
                    Logout
                  </v-list-item-title>
                </v-list-item>
              </v-list>
            </v-menu>
          </div>
        </div>
      </template> -->
    </v-app-bar>

    <v-navigation-drawer app v-model="drawer" class="">
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="text-h6 mb-2">
            <v-icon medium color="" class=""> mdi-domain </v-icon>
            <span> ArchyStores </span>
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>
      <!--
      <v-divider></v-divider>

      <template v-slot:prepend>
        <v-list-item two-line>
          <v-list-item-avatar>
            <img src="https://randomuser.me/api/portraits/women/81.jpg">
          </v-list-item-avatar>

          <v-list-item-content>
            <v-list-item-title>Jane Smith</v-list-item-title>
            <v-list-item-subtitle>Logged In</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </template> -->

      <v-divider></v-divider>

      <v-list dense nav>
        <v-list-item
          v-for="eachSidebarListAndRoute in allSidebarListAndRoutes"
          :key="eachSidebarListAndRoute.title"
          link
          v-model="selectedItem"
          color="success"
          @click="changeRoutes(eachSidebarListAndRoute.route)"
        >
          <v-list-item-icon>
            <v-icon>{{ eachSidebarListAndRoute.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{
              eachSidebarListAndRoute.title
            }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>

      <template v-slot:append>
        <div class="pa-2">
          <v-btn block> Logout </v-btn>
        </div>
      </template>
    </v-navigation-drawer>
  </nav>
</template>

<script lang="js">
// import defineComponent from "vue";

export default {
  name: "Topbar",

  data: () => ({
    drawer: true,
    selectedItem: 0,
    allSidebarListAndRoutes: [
      {
        title: "Home",
        icon: "mdi-view-dashboard",
        route: "/home",
        // subItems: [
        //   {tit  le: "test Sub", icon: "mdi-home", route: "/home"}
        // ]
      },
      {
        title: "About",
        icon: "mdi-help-box",
        route: "/about",
      },
      {
        title: "Categories",
        icon: "mdi-help-box",
        route: "/categories",
      },
      // {
      //   title: "Store",
      //   icon: "mdi-help-box",
      //   route: "/store",
      // },
      {
        title: "New Product",
        icon: "mdi-view-dashboard",
        route: "/new-product/",
      },
    ],
    right: null,
  }),

  components: {},

  methods: {
    changeRoutes(route) {
      this.$router.push(route);
      console.log(route);
      console.log(this.$route.params) 
    },
  },

  created() {
    console.log(this.$router.params.product_id)
  },
};
</script>




<style scoped>
/*
 <!-- <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar> -->

*/
</style>