<template>
  <v-containner>
    <paystack
      :amount="amount * 100"
      :email="email"
      :paystackkey="PUBLIC_KEY"
      :reference="reference"
      :callback="processPayment"
      :close="close"
    >
      Make Payment
    </paystack>
  </v-containner>
</template>

<script>
import paystack from 'vue-paystack'

export default {
  name: 'App',
  components: {
    paystack,
  },
  data: () => {
    return {
      amount: 90,
      full_name: "Archyscript",
      email: "yungdansa@gmail.com",
      PUBLIC_KEY: "pk_test_3af5f370ab741fb7ce7d5f574dab3659a24a8048"
    }
  },

  computed: {
    reference() {
      let text = ''
      let possible =
        'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789'
      for (let i = 0; i < 10; i++)
        text += possible.charAt(Math.floor(Math.random() * possible.length))
      return text
    },
  },
  methods: {
    processPayment: () => {
      window.alert('Payment recieved')
    },
    close: () => {
      console.log('You closed checkout page')
    },
  },
}
</script>
