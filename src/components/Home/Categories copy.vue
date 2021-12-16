<template>
  <div>
    <v-container>
      <v-row justify="center">
        <v-col cols="12" class="text-center">
          <v-subheader class="text-h4 justify-center">Categories</v-subheader>
        </v-col>

        <v-col cols="12">
          <div class="text-center">
            <!-- <v-btn
              @click="activeCategory = 'simple_app'"
              :color="activeCategory == 'simple_app' ? 'success' : ''"
              class="mx-2 px-3 mb-3"
              outlined
            >
              New Product
            </v-btn> -->
            <!-- <v-btn
              @click="activeCategory = 'simple_app'"
              :color="activeCategory == 'simple_app' ? 'success' : ''"
              class="mx-2 px-3 mb-3"
              outlined
            >
              Simple App
            </v-btn> -->
            <!--
            <v-btn
              @click="activeCategory = 'instrument'"
              :color="activeCategory == 'instrument' ? 'success' : ''"
              class="mx-2 px-3 mb-3"
              outlined
            >
              Instruments
            </v-btn>
            <v-btn
              @click="activeCategory = 'clone'"
              :color="activeCategory == 'clone' ? 'success' : ''"
              class="mx-2 px-3 mb-3"
              outlined
            >
              Clone Sites
            </v-btn> -->
          </div>
        </v-col>

<v-col col="12">
          <v-row justify="center">
            <v-col
              v-for="eachProduct in allAvailableProducts"
              :key="eachProduct._id"
              cols="12"
              sm="6"
              md="4"
            >
              <!-- <template v-if="eachProduct.available"> -->
              <v-card>
                <v-img
                  :src="eachProduct.product_image_details.src"
                  class="white--text align-end"
                  gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                  height="200px"
                >
                  <template v-slot:placeholder>
                    <v-row
                      class="fill-height ma-0"
                      align="center"
                      justify="center"
                    >
                      <v-progress-circular
                        indeterminate
                        color="grey lighten-5"
                      ></v-progress-circular>
                    </v-row>
                  </template>
                  <v-card-title class="text-h5 font-weight-bold">
                    {{ eachProduct.product_name }}
                  </v-card-title>
                </v-img>

                <v-card-actions>
                  <v-btn color="orange lighten-2" text>Description</v-btn>

                  <v-spacer></v-spacer>

                  <v-btn icon @click="showDescription(eachProduct.product_name)">
                    <v-icon>
                      {{
                        eachProduct.title === productId
                          ? 'mdi-chevron-up'
                          : 'mdi-chevron-down'
                      }}
                    </v-icon>
                  </v-btn>
                </v-card-actions>

                <v-expand-transition>
                  <div v-show="eachProduct.title === productId">
                    <v-card-text>
                      {{ eachProduct.description }}
                    </v-card-text>
                  </div>
                </v-expand-transition>
              </v-card>

              <v-divider></v-divider>

              <v-card-actions>
                <v-btn
                  color="teal darken-3"
                  @click="viewProductDetails(eachProduct)"
                  outlined
                  text
                >
                  View Details
                  <v-icon right dark>mdi-information-variant</v-icon>
                </v-btn>

                <v-spacer></v-spacer>

                <v-btn
                  color="dark"
                  @click="addItemToCart(eachProduct)"
                  outlined
                  text
                >
                  Add Cart
                  <v-icon right dark>mdi-cart-variant</v-icon>
                </v-btn>
              </v-card-actions>
              <!-- </template> -->
            </v-col>
          </v-row>
        </v-col>

        <v-dialog v-model="dialog" persistent max-width="80%">
          <v-card>
            <v-row>
              <v-col>
                <v-img
                  src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
                  class="white--text align-end"
                  gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                  height="400px"
                >
                  <template v-slot:placeholder>
                    <v-row
                      class="fill-height ma-0"
                      align="center"
                      justify="center"
                    >
                      <v-progress-circular
                        indeterminate
                        color="grey lighten-5"
                      ></v-progress-circular>
                    </v-row>
                  </template>
                </v-img>
              </v-col>

              <v-col></v-col>
            </v-row>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn danger outlined text @click="dialog = false">
                Close
              </v-btn>
              <!-- <v-btn color="green darken-1" text @click="dialog = false">
                Agree
              </v-btn> -->
            </v-card-actions>
          </v-card>
        </v-dialog>

        <v-col col="12" class="d-none">
          <v-row justify="center" v-if="activeCategory == 'simple_app'">
            <v-col
              v-for="simple_app in simple_apps"
              :key="simple_app.title"
              cols="12"
              sm="6"
              md="4"
            >
              <!-- <template v-if="simple_app.available"> -->
              <v-card>
                <v-img
                  :src="simple_app.src"
                  class="white--text align-end"
                  gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                  height="200px"
                >
                  <template v-slot:placeholder>
                    <v-row
                      class="fill-height ma-0"
                      align="center"
                      justify="center"
                    >
                      <v-progress-circular
                        indeterminate
                        color="grey lighten-5"
                      ></v-progress-circular>
                    </v-row>
                  </template>
                  <v-card-title class="text-h5 font-weight-bold">
                    {{ simple_app.title }}
                  </v-card-title>
                </v-img>

                <v-card-actions>
                  <v-btn color="orange lighten-2" text>Description</v-btn>

                  <v-spacer></v-spacer>

                  <v-btn icon @click="showDescription(simple_app.title)">
                    <v-icon>
                      {{
                        simple_app.title === productId
                          ? 'mdi-chevron-up'
                          : 'mdi-chevron-down'
                      }}
                    </v-icon>
                  </v-btn>
                </v-card-actions>

                <v-expand-transition>
                  <div v-show="simple_app.title === productId">
                    <v-card-text>
                      {{ simple_app.description }}
                    </v-card-text>
                  </div>
                </v-expand-transition>
              </v-card>

              <v-divider></v-divider>

              <v-card-actions>
                <v-btn
                  color="teal darken-3"
                  @click="viewProductDetails(simple_app)"
                  outlined
                  text
                >
                  View Details
                  <v-icon right dark>mdi-information-variant</v-icon>
                </v-btn>

                <v-spacer></v-spacer>

                <v-btn
                  color="dark"
                  @click="addItemToCart(simple_app)"
                  outlined
                  text
                >
                  Add Cart
                  <v-icon right dark>mdi-cart-variant</v-icon>
                </v-btn>
              </v-card-actions>
              <!-- </template> -->
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script lang="">
import axios from 'axios'

export default {
  name: 'Portfolio',
  data: () => ({
    productId: '',
    BASE_URL:
      'https://archyscript-e-commerce-backend.herokuapp.com/api/products',
    activeCategory: 'simple_app',
    dialog: false,
    allAvailableProducts: [],
    simple_apps: [
      {
        title: 'Typing Game',
        description: `A typiing game that helps it's users improve their typing skills... A point is giving for each successfully typed word and a countdown timer is set... The user can has the option to selectselect different level and  each of this levels have varying countdown timer`,
        // description: `["item 1", "item 2", "item 3"] ... responsivenes : ["monile", "desktop"]`,
        techs: [{ title: 'HTML', icon: 'mdi-home', ratio: '' }],
        link: {
          deployed: 'https://archyscript-typing-game.netlify.app/',
          github: 'https://github.com/ArchyScript/typing_game.git',
          citonhub: 'https://www.citonhub.com/run-panel/692471289',
        },
        src: '',
        available: true,
      },
      {
        title: 'Simple Store',
        description: `A simple store that allows it users ... create a PRODUCER account and login with the details to add product to the store ... add available product in store to CART and purchase them...  This store demo doesn't use a backend or any database technology to store data, rather, it uses the inbuilt browsers LocalStorage (NOT A REAlTIME DATABASE) to store data temporarily`,
        // description: `["item 1", "item 2", "item 3"]`,
        techs: [{ title: 'HTML', icon: 'mdi-home', ratio: '' }],
        link: {
          deployed: 'https://archyscript-simple-store.netlify.app/',
          github: 'https://github.com/ArchyScript/simple_store.git',
          citonhub: '',
        },
        src: '',
        available: true,
      },
      {
        title: 'Random Quote Generator',
        description: `Genarates random quote for users`,
        // description: `["item 1", "item 2", "item 3"]`,
        techs: [{ title: 'HTML', icon: 'mdi-home', ratio: '' }],
        link: {
          deployed: 'https://archyscript-quote-generator.netlify.app/',
          github: 'https://github.com/ArchyScript/random_quote_generator.git',
          citonhub: '',
        },
        src: '',
        available: true,
      },
    ],

    clones: [
      {
        title: 'Airbnb',
        description: `An Airbnb clone... not very responsive though (best viewed on desktop or tablet)`,
        // description: `["item 1", "item 2", "item 3"]`,
        techs: [{ title: 'HTML', icon: 'mdi-home', ratio: '' }],
        link: {
          deployed: 'https://archyscript-airbnb-clone.netlify.app/',
          github: 'https://github.com/ArchyScript/airbnb_clone.git',
          citonhub: '',
        },
        src: '',
        available: true,
      },
      {
        title: 'Gmail Clone',
        description: `A Gmail clone with a darkmode feature... best viewed on tablet and dektop`,
        // description: `["item 1", "item 2", "item 3"]`,
        techs: [{ title: 'HTML', icon: 'mdi-home', ratio: '' }],
        link: {
          deployed: 'https://archyscript-gmail-clone.netlify.app/',
          github: 'https://github.com/ArchyScript/gmail_clone.git',
          citonhub: '',
        },
        src: '',
        available: true,
      },
    ],

    instruments: [
      {
        title: 'My Portfolio',
        description: `My portfolio website which includes programming languages I uses and their ratings accordingly... my contact info etc. (same as this page)`,
        // description: `["item 1", "item 2", "item 3"]`,
        techs: [{ title: 'HTML', icon: 'mdi-home', ratio: '' }],
        link: {
          deployed: 'https://archyscript-portfolio.netlify.app/',
          github: 'https://github.com/ArchyScript',
          citonhub: '',
        },
        src: '',
        available: true,
      },
    ],
  }),

  created() {
    axios
      .get(this.BASE_URL)
      .then((response) => {
        this.allAvailableProducts = response.data
        console.log(this.allAvailableProducts)
      })
      .catch((error) => {
        console.log(error)
      })
  },

  methods: {
    gotoLinkAddress(link) {
      window.open(link, '_blank')
    },
    viewProductDetails(product) {
      // this.dialog = true
      console.log(product)
    },
    showDescription(title) {
      if (this.productId == title) return (this.productId = '')
      if (this.productId != title) return (this.productId = title)
    },
    addItemToCart(product) {
      console.log(product)
    },
  },
}
</script>

<style lang="css" scoped></style>
