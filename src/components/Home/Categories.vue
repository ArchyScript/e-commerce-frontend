<template>
  <div>
    <v-container>
      <v-row justify="center">
        <v-col cols="12" class="text-center">
          <v-subheader class="text-h4 justify-center">Categories</v-subheader>
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

                  <v-btn icon @click="showDescription(eachProduct._id)">
                    <v-icon>
                      {{
                        eachProduct._id === productId
                          ? 'mdi-chevron-up'
                          : 'mdi-chevron-down'
                      }}
                    </v-icon>
                  </v-btn>
                </v-card-actions>

                <v-expand-transition>
                  <div v-show="eachProduct._id === productId">
                    <v-card-text>
                      {{ eachProduct.description }}
                    </v-card-text>
                  </div>
                </v-expand-transition>
              </v-card>

              <v-divider></v-divider>

              <v-card-actions>
                <!-- <v-spacer></v-spacer> -->
                <v-dialog
                  v-model="productDetailsDialog"
                  persistent
                  max-width="600px"
                  width="80%"
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-btn
                      color="dark"
                      @click="buyProduct(eachProduct)"
                      outlined
                      text
                      v-bind="attrs"
                      v-on="on"
                    >
                      Buy Now
                      <v-icon right dark>mdi-cart-variant</v-icon>
                    </v-btn>
                  </template>

                  <v-card>
                    <v-card-title>
                      <span class="text-h5">Product Details</span>
                    </v-card-title>

                    <v-col cols="12">
                      <v-img
                        :src="selectedtProductForPurchase.product_image"
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
                      </v-img>
                    </v-col>

                    <v-col cols="12">
                      <v-card-text>
                        <v-container>
                          <v-row>
                            <v-col cols="12">
                              <strong>Product Name</strong>
                              :
                              <span>
                                {{ selectedtProductForPurchase.product_name }}
                              </span>
                            </v-col>
                            <v-col cols="12">
                              <strong>Product Description</strong>
                              :
                              <span>
                                {{ selectedtProductForPurchase.description }}
                              </span>
                            </v-col>

                            <v-col cols="12">
                              <h5>Purchase Details</h5>

                              <v-row>
                                <v-col cols="12">
                                  <v-text-field
                                    type="number"
                                    :value="selectedtProductForPurchase.price"
                                    v-model="selectedtProductForPurchase.price"
                                    label="Price ($)"
                                    outlined
                                    filled
                                  ></v-text-field>
                                </v-col>

                                <v-col cols="12">
                                  <v-text-field
                                    type="number"
                                    :value="quantityPurchased"
                                    append-icon="mdi-dollar"
                                    v-model="quantityPurchased"
                                    label="Quantity"
                                    outlined
                                    @input="calculateAmount"
                                    filled
                                  ></v-text-field>
                                </v-col>

                                <v-col cols="12">
                                  <v-text-field
                                    type="number"
                                    :value="amount"
                                    v-model="amount"
                                    label="Amount ($)"
                                    append-icon="mdi-dollar"
                                    outlined
                                    disabled
                                    filled
                                  ></v-text-field>
                                </v-col>
                              </v-row>
                            </v-col>

                            <v-col cols="12">
                              <h5>User Details</h5>

                              <v-row>
                                <v-col cols="12">
                                  <v-text-field
                                    :value="fullName"
                                    v-model="fullName"
                                    placeholder="Full Name"
                                    label="Full Name"
                                    outlined
                                    filled
                                  ></v-text-field>
                                </v-col>

                                <v-col cols="12">
                                  <v-text-field
                                    :value="email"
                                    v-model="email"
                                    label="Email"
                                    placeholder="Email"
                                    outlined
                                    filled
                                  ></v-text-field>
                                </v-col>
                              </v-row>
                            </v-col>
                          </v-row>
                        </v-container>
                      </v-card-text>

                      <v-card-actions>
                        <v-spacer></v-spacer>
                        <v-btn
                          color="danger darken-1"
                          text
                          @click="productDetailsDialog = false"
                          outlined
                        >
                          Close
                        </v-btn>

                        <!-- <v-btn
                          color="success darken-1"
                          text
                          outlined
                          @click="proceedToMakePayment"
                        >
                          Pay with {{ paymentMethod.method }}
                        </v-btn> -->

                        <v-btn color="success darken-1" text outlined>
                          <paystack
                            :amount="amount * 100"
                            :email="email"
                            :paystackkey="PUBLIC_KEY"
                            :reference="reference"
                            :callback="processPayment"
                            :close="close"
                          >
                            Pay With Paystack
                          </paystack>
                        </v-btn>
                      </v-card-actions>
                    </v-col>
                  </v-card>
                </v-dialog>
              </v-card-actions>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>

    <!-- <paystack
      :amount="amount * 100"
      :email="email"
      :paystackkey="PUBLIC_KEY"
      :reference="reference"
      :callback="processPayment"
      :close="close"
    >
      Make Payment
    </paystack> -->
  </div>
</template>

<script lang="">
import axios from 'axios'
import paystack from 'vue-paystack'

export default {
  name: 'Portfolio',
  components: {
    paystack,
  },
  data: () => ({
    productId: '',
    productSuccessfullyAdded: false,
    productAlreadyInCart: false,
    productDetailsDialog: false,
    BASE_URL: '',
    activeCategory: 'simple_app',
    PUBLIC_KEY: '',
    dialog: false,
    email: '',
    fullName: '',
    allProductsInCart: [],
    allAvailableProducts: [],
    selectedtProductForPurchase: {
      product_id: 'product id',
      product_image: 'product image url',
      product_name: 'product name',
      product_description: 'product description',
      price: 0,
      quantity: 1,
    },
    quantityPurchased: 1,
    amount: 1,
    paymentMethod: { method: 'paystack', details: '' },
    paymentMethods: [
      { method: 'stripe', details: '' },
      { method: 'paypal', details: '' },
      { method: 'paystack', details: '' },
      { method: 'flutterwave', details: '' },
    ],
    processPaymentBoolean: true,
  }),

  computed: {
    // this.amount  = this      .
    reference() {
      // this.email = this.email
      let text = ''
      let possible =
        'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789'
      for (let i = 0; i < 10; i++)
        text += possible.charAt(Math.floor(Math.random() * possible.length))

      return text
    },

    // calculateAmount() {
    //   // `this` points to the vm instance
    //   // return this.message.split('').reverse().join('')
    //   return this.amount = this.quantityPurchased * this.selectedtProductForPurchase.price
    // }
  },

  // watch: {
  // calculateAmount: {
  //   deep: true,
  // handler: function (newVal) {
  //   this.selected = newVal[0]
  //   this.allKeys = newVal
  // }
  // }
  // },

  created() {
    this.BASE_URL = this.$BASE_URL
    this.PUBLIC_KEY = this.$PUBLIC_KEY
    // console.log(paystack)
    console.log(this.BASE_URL)

    axios
      .get(this.BASE_URL, {
        params: {
          _limit: 2
        }
      })
      .then((response) => {
        this.allAvailableProducts = response.data
        console.log(this.allAvailableProducts)
      })
      .catch((error) => {
        console.log(error)
      })
  },

  methods: {
    viewProductDetails(product) {
      // this.dialog = true
      console.log(product)
    },
    processPayment: () => {
      window.alert('Payment recieved')
      // this.$router.push({ path: `/home` })
    },
    close: () => {
      console.log('You closed checkout page')
    },
    calculateAmount() {
      return (this.amount =
        this.quantityPurchased * this.selectedtProductForPurchase.price)
    },
    buyProduct(product) {
      // this.dialog = true
      this.calculateAmount()
      console.log(product)
      this.selectedtProductForPurchase.product_name = product.product_name
      this.selectedtProductForPurchase.description = product.description
      this.selectedtProductForPurchase.price = product.product_details.price
      this.selectedtProductForPurchase.quantity =
        product.product_details.quantity
      this.selectedtProductForPurchase.product_image = product.product_image
    },
    afterPaymentFunction() {
      this.selectedtProductForPurchase = {
        product_id: '',
        product_image: '',
        product_name: '',
        product_description: '',
        price: 0,
        quantity: 1,
      }
    },
    proceedToMakePayment() {
      this.productDetailsDialog = false
      // this.processPayment = true

      this.$router.push({ path: `/payment/${this.paymentMethod.method}` })
    },
    showDescription(product_id) {
      console.log(product_id)
      if (this.productId == product_id) return (this.productId = '')
      if (this.productId != product_id) return (this.productId = product_id)
    },
    addItemToCart(product) {
      console.log(product)

      // this.allProductsInCart.forEach(eachProductInCart => {
      //   if (eachProductInCart._id == product._id) {
      //     console.log("testing")
      //   } else {
      //     this.allProductsInCart.push(product)
      //   }
      // })
      if (this.allProductsInCart.length < 1) {
        this.productSuccessfullyAdded = true
        return this.allProductsInCart.push(product)
      }

      this.allProductsInCart.forEach((eachProductInCart) => {
        if (eachProductInCart._id == product._id) {
          return (this.productAlreadyInCart = true)
        } else {
          this.productSuccessfullyAdded = true
        }
      })
      this.allProductsInCart.push(product)
      console.log(this.allProductsInCart)

      setTimeout(() => {
        this.productSuccessfullyAdded = false
        this.productAlreadyInCart = false
      }, 3000)
      // setTimeout(() => (this.productSuccessfullyAdded = false), 3000)
    },
  },
}
</script>

<style lang="css" scoped></style>
