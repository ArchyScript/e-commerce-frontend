<template>
  <div>
    <v-container>
      <v-row justify="center">
        <v-col cols="12" class="text-center">
          <v-subheader class="text-h4 justify-center"> Portfolio </v-subheader>
        </v-col>

        <v-col cols="12">
          <div class="text-center">
            <v-chip
              @click="activePortfolio = 'desktop_app'"
              :color="activePortfolio == 'desktop_app' ? 'success' : ''"
              class="mx-2 px-3 mb-3"
              outlined
            >
              Desktop App
            </v-chip>
            <v-chip
              @click="activePortfolio = 'clone'"
              :color="activePortfolio == 'clone' ? 'success' : ''"
              class="mx-2 px-3 mb-3"
              outlined
            >
              Clone Sites
            </v-chip>
            <v-chip
              @click="activePortfolio = 'simple_app'"
              :color="activePortfolio == 'simple_app' ? 'success' : ''"
              class="mx-2 px-3 mb-3"
              outlined
            >
              Simple App
            </v-chip>
          </div>
        </v-col>

        <v-col col="12">
          <v-row justify="center" v-if="activePortfolio == 'simple_app'">
            <v-col
              v-for="simple_app in simple_apps"
              :key="simple_app.title"
              cols="12"
              sm="6"
              md="4"
              lg="3"
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
                  <v-btn color="orange lighten-2" text> Description </v-btn>

                  <v-spacer></v-spacer>

                  <v-btn icon @click="showDescription(simple_app.title)">
                    <v-icon>
                      {{
                        simple_app.title === projectTitle
                          ? "mdi-chevron-up"
                          : "mdi-chevron-down"
                      }}
                    </v-icon>
                  </v-btn>
                </v-card-actions>

                <v-expand-transition>
                  <div v-show="simple_app.title === projectTitle">
                    <v-divider></v-divider>

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
                  outlined
                  text
                  @click="gotoLinkAddress(simple_app.link.deployed)"
                >
                  Preview
                  <v-icon right dark> mdi-open-in-new </v-icon>
                </v-btn>

                <v-btn
                  color="dark"
                  outlined
                  text
                  @click="gotoLinkAddress(simple_app.link.github)"
                >
                  Github
                  <v-icon right dark> mdi-github </v-icon>
                </v-btn>
              </v-card-actions>
              <!-- </template> -->
            </v-col>
          </v-row>

          <v-row justify="center" v-if="activePortfolio == 'clone'">
            <v-col
              v-for="clone in clones"
              :key="clone.title"
              cols="12"
              sm="6"
              md="4"
              lg="3"
            >
              <!-- <template v-if="clone.available"> -->
              <v-card>
                <v-img
                  :src="clone.src"
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
                    {{ clone.title }}
                  </v-card-title>
                </v-img>

                <v-card-actions>
                  <v-btn color="orange lighten-2" text> Description </v-btn>

                  <v-spacer></v-spacer>

                  <v-btn icon @click="showDescription(clone.title)">
                    <v-icon>
                      {{
                        clone.title === projectTitle
                          ? "mdi-chevron-up"
                          : "mdi-chevron-down"
                      }}
                    </v-icon>
                  </v-btn>
                </v-card-actions>

                <v-expand-transition>
                  <div v-show="clone.title === projectTitle">
                    <v-divider></v-divider>

                    <v-card-text>
                      {{ clone.description }}
                    </v-card-text>
                  </div>
                </v-expand-transition>
              </v-card>

              <v-divider></v-divider>

              <v-card-actions>
                <v-btn
                  color="teal darken-3"
                  outlined
                  text
                  @click="gotoLinkAddress(clone.link.deployed)"
                >
                  Preview
                  <v-icon right dark> mdi-open-in-new </v-icon>
                </v-btn>

                <v-btn
                  color="dark"
                  outlined
                  text
                  @click="gotoLinkAddress(clone.link.github)"
                >
                  Github
                  <v-icon right dark> mdi-github </v-icon>
                </v-btn>
              </v-card-actions>
              <!-- </template> -->
            </v-col>
          </v-row>

          <v-row justify="center" v-if="activePortfolio == 'desktop_app'">
            <v-col
              v-for="desktop_app in desktop_apps"
              :key="desktop_app.title"
              cols="12"
              sm="6"
              md="4"
              lg="3"
            >
              <!-- <template v-if="desktop_app.available"> -->
              <v-card>
                <v-img
                  :src="desktop_app.src"
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
                    {{ desktop_app.title }}
                  </v-card-title>
                </v-img>

                <v-card-actions>
                  <v-btn color="orange lighten-2" text> Description </v-btn>

                  <v-spacer></v-spacer>

                  <v-btn icon @click="showDescription(desktop_app.title)">
                    <v-icon>
                      {{
                        desktop_app.title === projectTitle
                          ? "mdi-chevron-up"
                          : "mdi-chevron-down"
                      }}
                    </v-icon>
                  </v-btn>
                </v-card-actions>

                <v-expand-transition>
                  <div v-show="desktop_app.title === projectTitle">
                    <v-divider></v-divider>

                    <v-card-text>
                      {{ desktop_app.description }}
                    </v-card-text>
                  </div>
                </v-expand-transition>
              </v-card>

              <v-divider></v-divider>

              <v-card-actions>
                <v-btn
                  color="teal darken-3"
                  outlined
                  text
                  @click="gotoLinkAddress(desktop_app.link.deployed)"
                >
                  Preview
                  <v-icon right dark> mdi-open-in-new </v-icon>
                </v-btn>

                <v-btn
                  color="dark"
                  outlined
                  text
                  @click="gotoLinkAddress(desktop_app.link.github)"
                >
                  Github
                  <v-icon right dark> mdi-github </v-icon>
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
export default {
  name: "Portfolio",
  data: () => ({
    projectTitle: "",
    activePortfolio: "desktop_app",
    simple_apps: [
      {
        title: "Typing Game",
        description: `A typiing game that helps it's users improve their typing skills... A point is giving for each successfully typed word and a countdown timer is set... The user can has the option to selectselect different level and  each of this levels have varying countdown timer`,
        // description: `["item 1", "item 2", "item 3"] ... responsivenes : ["monile", "desktop"]`,
        techs: [{ title: "HTML", icon: "mdi-home", ratio: "" }],
        link: {
          deployed: "https://archyscript-typing-game.netlify.app/",
          github: "https://github.com/ArchyScript/typing_game.git",
          citonhub: "https://www.citonhub.com/run-panel/692471289",
        },
        src: require("@/img/portfolio/typing_game.png"),
        available: true,
      },
      {
        title: "Simple Store",
        description: `A simple store that allows it users ... create a PRODUCER account and login with the details to add product to the store ... add available product in store to CART and purchase them...  This store demo doesn't use a backend or any database technology to store data, rather, it uses the inbuilt browsers LocalStorage (NOT A REAlTIME DATABASE) to store data temporarily`,
        // description: `["item 1", "item 2", "item 3"]`,
        techs: [{ title: "HTML", icon: "mdi-home", ratio: "" }],
        link: {
          deployed: "https://archyscript-simple-store.netlify.app/",
          github: "https://github.com/ArchyScript/simple_store.git",
          citonhub: "",
        },
        src: require("@/img/portfolio/store.png"),
        available: true,
      },
      {
        title: "Tic Tac Toe Game",
        description: `A TIC TAC TOE game that allows it users set player names, keep track of players score, detects if a particular game is a tie and reset players score`,
        // description: `["item 1", "item 2", "item 3"]`,
        techs: [{ title: "HTML", icon: "mdi-home", ratio: "" }],
        link: {
          deployed: "https://archyscript-tic-tac-toe-game.netlify.app/",
          github: "https://github.com/ArchyScript/tic-tac-toe-game.git",
          citonhub: "https://www.citonhub.com/run-panel/325777815",
        },
        src: require("@/img/portfolio/tic_tac_toe.png"),
        available: true,
      },
      {
        title: "Simple Responsive Dashboard",
        description: `A simple responsive dashboard design`,
        // description: `["item 1", "item 2", "item 3"]`,
        techs: [{ title: "HTML", icon: "mdi-home", ratio: "" }],
        link: {
          deployed: "https://simple-responsive-dashboard.netlify.app/",
          github:
            "https://github.com/ArchyScript/simple_responsive_dashboard.git",
          citonhub: "",
        },
        src: require("@/img/portfolio/simple_dashboard.png"),
        available: true,
      },
      {
        title: "Simple Calculator",
        description: `A simple calculator that can perform all basic arithmetic operations.`,
        // description: `["item 1", "item 2", "item 3"]`,
        techs: [{ title: "HTML", icon: "mdi-home", ratio: "" }],
        link: {
          deployed: "https://archyscript-simple-calculator.netlify.app/",
          github: "https://github.com/ArchyScript/simple_calculator.git",
          citonhub: "",
        },
        src: require("@/img/portfolio/simple_calculator.png"),
        available: true,
      },
      {
        title: "Virtual Keyboard",
        description: `A virtual keyboard that allows user type words and displays output for the user... User can change keyboard colour, height, fonts etc.`,
        // description: `["item 1", "item 2", "item 3"]`,
        techs: [{ title: "HTML", icon: "mdi-home", ratio: "" }],
        link: {
          deployed: "https://archyscript-virtual-keyboard.netlify.app/",
          github: "https://github.com/ArchyScript/virtual_keyboard.git",
          citonhub: "",
        },
        src: require("@/img/portfolio/virtual_keyboard.png"),
        available: true,
      },
      {
        title: "Random Quote Generator",
        description: `Genarates random quote for users`,
        // description: `["item 1", "item 2", "item 3"]`,
        techs: [{ title: "HTML", icon: "mdi-home", ratio: "" }],
        link: {
          deployed: "https://archyscript-quote-generator.netlify.app/",
          github: "https://github.com/ArchyScript/random_quote_generator.git",
          citonhub: "",
        },
        src: require("@/img/portfolio/random_quote.png"),
        available: true,
      },
      {
        title: "Promise Card",
        description: `A simple promise card design which allows user change background colour`,
        // description: `["item 1", "item 2", "item 3"]`,
        techs: [{ title: "HTML", icon: "mdi-home", ratio: "" }],
        link: {
          deployed: "https://archyscript-promise-card.netlify.app/",
          github: "https://github.com/ArchyScript/promise_card.git",
          citonhub: "",
        },
        src: require("@/img/portfolio/promise_card.png"),
        available: true,
      },
      {
        title: "Matrix Calculator",
        description: `An app that is capable of solving basic 3x3 matrix problems... Ranging from the determinat, transpose, adjoint to the inverse of that matrix.`,
        // description: `["item 1", "item 2", "item 3"]`,
        techs: [{ title: "HTML", icon: "mdi-home", ratio: "" }],
        link: {
          deployed: "https://archyscript-matrix-calculator.netlify.app/",
          github: "https://github.com/ArchyScript/matrrix_calculator.git",
          citonhub: "",
        },
        src: require("@/img/portfolio/matrix_calculator.png"),
        available: true,
      },
      {
        title: "Lenght Converter",
        description: `An app that can perform some basic unnit conversion... Also allows user select a unit as reference and base scale for other units...v User can also switch convertion scale`,
        // description: `["item 1", "item 2", "item 3"]`,
        techs: [{ title: "HTML", icon: "mdi-home", ratio: "" }],
        link: {
          deployed: "https://archyscript-lenght-converter.netlify.app/",
          github: "https://github.com/ArchyScript/lenght_converter.git",
          citonhub: "https://www.citonhub.com/run-panel/012931123",
        },
        src: require("@/img/portfolio/lenght_converter.png"),
        available: true,
      },
      // {
      //   title: "Ludo Game",
      //   description: ``,
      // description: `["item 1", "item 2", "item 3"]`,
      //     techs: [
      // {title: "HTML", icon: "mdi-home", ratio: ""}
      //     ],
      //      link: {
      //     deployed: "",
      //     github: "",
      //     citonhub: "",
      //   },
      //   src: require("@/img/portfolio/tic_tac_toe.png"),
      //   available: true,
      // },
      // {
      //   title: "Text Editor",
      //   description: ``,      //
      // description: `["item 1", "item 2", "item 3"]`,
      // techs: [
      //   {title: "HTML", icon: "mdi-home", ratio: ""}
      // ],
      //  link: {
      //     deployed: "",
      //     github: "https://github.com/ArchyScript/text_editor.git",
      //     citonhub: "",
      //   },
      //   src: require("@/img/portfolio/tic_tac_toe.png"),
      //   available: true,
      // },
    ],

    clones: [
      {
        title: "Airbnb",
        description: `An Airbnb clone... not very responsive though (best viewed on desktop or tablet)`,
        // description: `["item 1", "item 2", "item 3"]`,
        techs: [{ title: "HTML", icon: "mdi-home", ratio: "" }],
        link: {
          deployed: "https://archyscript-airbnb-clone.netlify.app/",
          github: "https://github.com/ArchyScript/airbnb_clone.git",
          citonhub: "",
        },
        src: require("@/img/portfolio/airbnb.png"),
        available: true,
      },
      {
        title: "Gmail Clone",
        description: `A Gmail clone with a darkmode feature... best viewed on tablet and dektop`,
        // description: `["item 1", "item 2", "item 3"]`,
        techs: [{ title: "HTML", icon: "mdi-home", ratio: "" }],
        link: {
          deployed: "https://archyscript-gmail-clone.netlify.app/",
          github: "https://github.com/ArchyScript/gmail_clone.git",
          citonhub: "",
        },
        src: require("@/img/portfolio/gmail.png"),
        available: true,
      },
    ],

    desktop_apps: [
      {
        title: "My Portfolio",
        description: `My portfolio website which includes programming languages I uses and their ratings accordingly... my contact info etc. (same as this page)`,
        // description: `["item 1", "item 2", "item 3"]`,
        techs: [{ title: "HTML", icon: "mdi-home", ratio: "" }],
        link: {
          deployed: "https://archyscript-portfolio.netlify.app/",
          github: "https://github.com/ArchyScript",
          citonhub: "",
        },
        src: require("@/assets/profile_picture.png"),
        available: true,
      },
    ],
  }),

  methods: {
    gotoLinkAddress(link) {
      window.open(link, "_blank");
      // window.location.href = link;
    },
    showDescription(title) {
      if (this.projectTitle == title) return (this.projectTitle = "");
      if (this.projectTitle != title) return (this.projectTitle = title);
    },
  },
};
</script>

<style lang="css" scoped>
/** /
.disable_btn {

} 
/**/
</style>