<template>
  <div block class="mx- auto align-center">
    <v-footer padless class="mt-6 mx-auto">
      <v-col cols="12">
        <v-row justify="center">
          <v-col cols="8" lg="6" class="text-center">
            <v-toolbar-title
              class="text-h4 success--text mt-4 justify-center"
              style="font-weight: 700"
            >
              ArchyScript
            </v-toolbar-title>

            <v-card-text class="my-1 justify-center">
              <v-btn
                v-for="socialMedia in socialMedias"
                :key="socialMedia.icon"
                class="mx-2 my-2 black--text"
                icon
                :color="socialMedia.color"
                @click="gotoLinkAddress(socialMedia.link)"
              >
                <v-icon size="1.8rem" outlined>
                  {{ socialMedia.icon }}
                </v-icon>
              </v-btn>
            </v-card-text>

            <v-subheader class="my-2 justify-center">
              Kindly connect with me on my social media platform by clicking any of the links above
            </v-subheader>


            <v-subheader class="mt-4 justify-center">
             <v-btn outlined :href="resumeLink" target="_blank" class="green--text">
                 VIEW RESUME 
              </v-btn> 
            </v-subheader>

            <!-- <v-form class="my-2 justify-center">
              <v-text-field
                outlined
                v-model="email"
                label="Subscribe for weekly news"
                required
                densed
              ></v-text-field>
              <v-btn
                outlined
                :class="emailIsValid ? '' : 'disabled'"
                color="success"
                >Subscribe</v-btn
              >
            </v-form> -->
          </v-col>
        </v-row>

        <v-divider></v-divider>

        <v-row justify="center">
          <v-col cols="8" lg="6" class="text-center">
            <v-subheader class="justify-center">
              Copyright ©
              {{ new Date().getFullYear() }} —
              <strong class="mx-1 success--text">ArchyScript</strong>
            </v-subheader>
          </v-col>
        </v-row>
      </v-col>
    </v-footer>
  </div>
</template>

<script>
export default {
  name: "Footer",
  data: () => ({
    emailIsValid: false,
    resumeLink:
      "https://www.canva.com/design/DAEuiM5OxmY/cGwVcE1sUqFEa0Ld9Pml0A/view?utm_content=DAEuiM5OxmY&utm_campaign=designshare&utm_medium=link&utm_source=sharebutton",
    socialMedias: [
      {
        color: "primary",
        icon: "mdi-facebook",
        link: "https://web.facebook.com/oluwatoyin.dasaolu.9/",
      },
      {
        color: "blue darken-1",
        icon: "mdi-twitter",
        link: "https://twitter.com/ArchyScript",
      },
      {
        color: "black",
        icon: "mdi-github",
        link: "https://github.com/ArchyScript",
      },
      {
        color: "primary",
        icon: "mdi-linkedin",
        link: "www.linkedin.com/in/archyscript",
      },
    ],
    email: "",
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
    ],
  }),
  methods: {
    gotoLinkAddress(link) {
      window.open(link, "_blank");
      // window.location.href = link;
    },
  },
};
</script>