<template>
  <div>
    <v-container fluid>
      <v-row dense>
        <v-col cols="12">
          <v-card>
            <v-img
              src="@/img/dark-1.jpeg"
              class="white--text align-end"
              gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
              height="120px"
            >
              <v-card-title> {{ title }} </v-card-title>
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
    title: "",
    imageSrc: "@/img/dark-2.jpeg",
  }),
};
</script>