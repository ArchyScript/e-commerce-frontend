<template>
  <div>
    <v-container fluid>
      <div class="text-center">
        <h3>Explore</h3>
      </div>

      <v-row justify="center" dense>
        <v-col v-for="card in cards" :key="card.id" cols="12" sm="6" lg="4">
          <v-card flat outlined>
            <v-img
              :src="card.src"
              class="white--text align-end"
              gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
              height="180px"
            >
            </v-img>

            <v-card-title> {{ card.title }} </v-card-title>
            <v-card-subtitle> {{ card.subtitle }} </v-card-subtitle>

            <v-card-text class="text--primary">
              <div>{{ card.description }}</div>
            </v-card-text>

            <v-card-actions>
              <v-btn color="orange" outlined text> Details </v-btn>

              <v-btn color="green" outlined text> Explore </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>

        <v-col cols="12" class="text-center">
          <v-btn outlined class="ma-2"> Explore Architecture </v-btn>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>


<script>
export default {
  data: () => ({
    cards: [
      {
        id: 1,
        title: "Home sweet home",
        subtitle: "Subtitle",
        description:
          "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Voluptas quisquam quo dignissimos ratione. Numquam accusantiumamet delectus quibusdam tenetur a.",
        src: "https://cdn.vuetifyjs.com/images/cards/house.jpg",
      },
      {
        id: 2,
        title: "Favorite road trips",
        subtitle: "Subtitle",
        description:
          "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Voluptas quisquam quo dignissimos ratione. Numquam accusantiumamet delectus quibusdam tenetur a.",
        src: "https://cdn.vuetifyjs.com/images/cards/road.jpg",
      },
      {
        id: 3,
        title: "Favorite road trips",
        subtitle: "Subtitle",
        description:
          "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Voluptas quisquam quo dignissimos ratione. Numquam accusantiumamet delectus quibusdam tenetur a.",
        src: "https://cdn.vuetifyjs.com/images/cards/road.jpg",
      },
      {
        id: 4,
        title: "Best airlines",
        subtitle: "Subtitle",
        description:
          "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Voluptas quisquam quo dignissimos ratione. Numquam accusantiumamet delectus quibusdam tenetur a.",
        src: "https://cdn.vuetifyjs.com/images/cards/plane.jpg",
      },
    ],
  }),
};
</script>