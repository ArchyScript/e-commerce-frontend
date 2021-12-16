
<template>
  <div>
    <v-container class="mt-6">
      <v-row justify="center">
        <v-col cols="12" class="text-center">
          <v-subheader class="text-h4 justify-center"> Contact </v-subheader>
        </v-col>

        <v-col cols="12">
          <v-alert
            type="success"
            v-model="alert"
            dismissible
            border="left"
            elevation="2"
          >
            Hey {{ alertName }} 😊😊, thank you for contacting me... I'll reply
            your email very soon
          </v-alert>
        </v-col>

        <v-col cols="12" md="6">
          <!-- <iframe
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d126831.27491032869!2d3.1802817048218786!3d6.5874336712680694!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x103b901f96e8c3e9%3A0xb8394a539887b0fe!2sAlimosho!5e0!3m2!1sen!2sng!4v1635185459834!5m2!1sen!2sng"
          width="100%"
          height="100%"
          style="border: 0"
          allowfullscreen=""
          loading="lazy"
        ></iframe> -->

          <iframe
            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d31644.426998692372!2d4.528531400820674!3d7.514453424817697!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x1038313bb9ddefb5%3A0x3fa6fa38284c1949!2sObafemi%20Awolowo%20University!5e0!3m2!1sen!2sng!4v1635185028964!5m2!1sen!2sng"
            width="100%"
            height="100%"
            style="border: 0; border: 2rem"
            allowfullscreen=""
            loading="lazy"
          ></iframe>
        </v-col>

        <v-col cols="12" md="6">
          <form
            id="contact-form"
            ref="form"
            @submit.prevent="sendEmail"
            lazy-validation
          >
            <v-text-field
              v-model="contactInfo.name"
              name="user_name"
              outlined
              label="Name"
              required
            ></v-text-field>

            <!--
            <v-text-field
              outlined
              v-model="contactInfo.mobileNumber"
              name="user_mobile_number"
              label="Mobile Nunber (optional)"
              type="number"
              required
            ></v-text-field> 
            -->

            <v-text-field
              outlined
              v-model="contactInfo.email"
              name="user_email"
              label="E-mail"
              required
            ></v-text-field>

            <v-textarea
              v-model="contactInfo.message"
              name="message"
              outlined
              auto-grow
              label="Drop your message..."
              rows="4"
              no-resize
            ></v-textarea>
            <!--
            <v-checkbox
              v-model="checkbox"
              :rules="[(v) => !!v || 'You must agree to continue!']"
              label="Check to confirm details"
              required
            ></v-checkbox>
            -->
            <div class="mt-3">
              <v-btn
                :loading="loading"
                color="success"
                outlined
                right
                class="mr-4"
                type="submit"
              >
                Contact
              </v-btn>
            </div>
          </form>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>


<script>
import emailjs from "emailjs-com";

export default {
  data: () => ({
    alert: false,
    loading: false,
    EMAILJS_SERVICE_ID: "service_b6xxwsr",
    EMAILJS_TEMPLATE_ID: "template_hhbp26e",
    EMAILJS_USER_ID: "user_fWc4DiIEXOB22gp3YINne",
    contactInfo: {
      name: "",
      email: "",
      message: "",
      // mobileNumber: "",
    },
    alertName: "",
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
    ],
    checkbox: false,
  }),
  methods: {
    sendEmail() {
      this.loading = true;
      this.alertName = this.contactInfo.name;
      emailjs
        .sendForm(
          this.EMAILJS_SERVICE_ID,
          this.EMAILJS_TEMPLATE_ID,
          this.$refs.form,
          this.EMAILJS_USER_ID
        )
        .then(
          () => {
            this.alert = true;
            this.loading = false;
            this.contactInfo.name = "";
            this.contactInfo.email = "";
            this.contactInfo.message = "";
          },
          () => {
            this.alert = false;
            this.loading = false;
          }
        );

      setTimeout(() => {
        this.alert = false;
      }, 10000);
    },
  },
};
</script>