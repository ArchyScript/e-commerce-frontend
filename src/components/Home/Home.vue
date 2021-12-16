<template>
  <div>
    <v-container fluid>
      <v-row justify="center" dense>
        <v-col cols="12">
          <v-card width="100%">
            <v-img
              :src="imageSrc"
              class="white--text align-end"
              gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
              height="500px"
            >
              <template v-slot:placeholder>
                <v-row class="fill-height ma-0" align="center" justify="center">
                  <v-progress-circular
                    indeterminate
                    color="success lighten-5"
                  ></v-progress-circular>
                </v-row>
              </template>
              <v-card-title class="text-h2 ml-8"> {{ title }} </v-card-title>
              <v-card-text
                class="white--text text-h5 ml-8"
                style="width: 60%; line-height: 3rem"
              >
                ...
                <span color="green-- text"> {{ randomText }} </span> providing
                all products for all architects
              </v-card-text>

              <v-card-action>
                <v-btn
                  outlined
                  class="white--text ml-12 mt-5 mb-10"
                  @click="$router.push('/architectures')"
                >
                  Get Started
                </v-btn>
              </v-card-action>

              <div class="mt-10"></div>
            </v-img>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>


<script>
export default {
  data: () => ({
    title: "Architecture Stores",
    imageSrce: "https://cdn.vuetifyjs.com/images/cards/house.jpg",
    imageSrc: require("@/img/dark-1.jpeg"),
    textColor: "green--text",
    randomText: "exploring",
    // randomTexts: ["exploring", "searching", "connecting"],
    // backgroundColors: [
    //   "orange",
    //   "lightgreen",
    //   "lightblue",
    //   "coral",
    //   "aqua",
    //   "magenta",
    //   "lime",
    //   "pink",
    //   "azure",
    //   "aliceblue",
    //   "beige",
    //   "bisque",
    //   "burlywood",
    //   "lightsalmon",
    //   "lavender",
    //   "orchid",
    //   "navajowhite",
    //   "mistyrose",
    //   "oldlace",
    //   "plum",
    //   "paleturquoise",
    // ],
  }),
  mounted() {
    // this.changeTextColor();
  },

  methods: {
    // changeTextColor() {
    //   let randomColorIndex = Math.floor(
    //     Math.random() * this.backgroundColors.length
    //   );
    //   let randomTextIndex = Math.floor(Math.random() * this.randomTexts.length);
    //   this.textColor = this.displayColors[randomColorIndex];
    // },
    /* 
  <template>
  <!-- Jumbotron -->
  <div
    class="card card-image mb-2"
    style="
      background-image: url(https://mdbcdn.b-cdn.net/img/Photos/Others/forest2.jpg);
    "
  >
    <div class="text-white text-center rgba-stylish-strong py-5 px-4">
      <div class="py-5">
        <!-- Content -->
        <h5 class="h5 orange-text">
          <i class="fas fa-camera-retro"></i> Photography
        </h5>
        <h2 class="card-title h2 my-4 py-2">Jumbotron with image overlay</h2>
        <p class="mb-4 pb-2 px-md-5 mx-md-5">
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Pariatur
          obcaecati vero aliquid libero doloribus ad, unde tempora maiores,
          ullam, modi qui quidem minima debitis perferendis vitae cumque et quo
          impedit.
        </p>
        <a class="btn peach-gradient"
          ><i class="fas fa-clone left"></i> View project</a
        >
      </div>
    </div>
  </div>
  <!-- Jumbotron -->
</template>
 */
  },
};
</script>

<style scoped>
</style>