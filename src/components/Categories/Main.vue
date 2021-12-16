<template>
  <div>
    <v-container>
      <v-row justify="center">
        <v-col cols="12" class="d-flex justify-content-between">
          <v-subheader class="text-h3 justify- center">Categories</v-subheader>

          <v-dialog
            v-model="newProductAdminAuthDialog"
            persistent
            max-width="600px"
            width="80%"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-btn color="success" outlined text v-bind="attrs" v-on="on">
                Add Product
                <v-icon right dark>mdi-plus</v-icon>
              </v-btn>
            </template>

            <v-card>
              <v-card-title>
                <span class="text-h5">Admin Login</span>
              </v-card-title>

              <v-col cols="12">
                <v-card-text>
                  <v-container>
                    <v-row>
                      <v-col cols="12">
                        <v-text-field
                          :value="adminUsername"
                          v-model="adminUsername"
                          label="Admin Username"
                          placeholder="Enter Admin Admin Username"
                          outlined
                          filled
                        ></v-text-field>
                      </v-col>

                      <v-col cols="12">
                        <v-text-field
                          type="password"
                          :value="adminPassword"
                          v-model="adminPassword"
                          label="Admin Password"
                          placeholder="Enter Admin Password"
                          outlined
                          filled
                        ></v-text-field>
                      </v-col>
                    </v-row>
                  </v-container>
                </v-card-text>

                <v-card-actions>
                  <v-btn
                    color="danger darken-1"
                    text
                    @click="newProductAdminAuthDialog = false"
                    outlined
                  >
                    Close
                  </v-btn>

                  <v-spacer></v-spacer>

                  <v-btn
                    color="danger darken-1"
                    text
                    @click="adminAuth"
                    outlined
                  >
                    Login
                  </v-btn>
                </v-card-actions>
              </v-col>
            </v-card>
          </v-dialog>
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
                <v-dialog
                  v-model="viewProductDetailsDialog"
                  persistent
                  max-width="600px"
                  width="80%"
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-btn
                      color="dark"
                      @click="viewProductDetails(eachProduct)"
                      outlined
                      text
                      v-bind="attrs"
                      v-on="on"
                    >
                      View Details
                      <v-icon right dark>mdi-cart-variant</v-icon>
                    </v-btn>
                  </template>

                  <v-card>
                    <v-card-title>
                      <span class="text-h5">Product Details</span>
                    </v-card-title>

                    <v-col cols="12">
                      <v-img
                        :src="selectedProduct.product_image_details.url"
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
                              <h5>Basic Details</h5>

                              <v-row>
                                <v-col cols="12">
                                  <strong>Product Name</strong>
                                  : {{ selectedProduct.product_name }}
                                </v-col>
                                <v-col cols="12">
                                  <strong>Product Description</strong>
                                  : {{ selectedProduct.description }}
                                </v-col>
                              </v-row>
                            </v-col>

                            <v-col cols="12">
                              <h5>Product Details</h5>

                              <v-row>
                                <v-col cols="12">
                                  <strong>Price</strong>
                                  : {{ selectedProduct.product_details.price }}
                                </v-col>
                                <v-col cols="12">
                                  <strong>Quantity</strong>
                                  :
                                  {{ selectedProduct.product_details.quantity }}
                                </v-col>
                                <v-col cols="12">
                                  <strong>Production Date</strong>
                                  : {{ selectedProduct.product_details.price }}
                                </v-col>
                                <v-col cols="12">
                                  <strong>Expiry Date</strong>
                                  : {{ selectedProduct.product_details.price }}
                                </v-col>
                              </v-row>
                            </v-col>

                            <v-col cols="12">
                              <h5>Address</h5>

                              <v-row>
                                <v-col cols="12">
                                  <strong>Postal Code</strong>
                                  : {{ selectedProduct.address.postal_code }}
                                </v-col>
                                <v-col cols="12">
                                  <strong>Location</strong>
                                  : {{ selectedProduct.address.location }}
                                </v-col>
                                <v-col cols="12">
                                  <strong>State</strong>
                                  : {{ selectedProduct.address.state }}
                                </v-col>
                                <v-col cols="12">
                                  <strong>Country</strong>
                                  : {{ selectedProduct.address.country }}
                                </v-col>
                              </v-row>
                            </v-col>

                            <v-col cols="12">
                              <h5>Contact Information</h5>

                              <v-row>
                                <v-col cols="12">
                                  <strong>Phone</strong>
                                  : {{ selectedProduct.contact_info.phone }}
                                </v-col>
                                <v-col cols="12">
                                  <strong>Email</strong>
                                  : {{ selectedProduct.contact_info.email }}
                                </v-col>
                                <v-col cols="12">
                                  <strong>Website Address</strong>
                                  :
                                  {{ selectedProduct.contact_info.website_url }}
                                </v-col>
                                <v-col cols="12">
                                  <strong>Website Title</strong>
                                  :
                                  {{
                                    selectedProduct.contact_info.website_title
                                  }}
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
                          @click="viewProductDetailsDialog = false"
                          outlined
                        >
                          Close
                        </v-btn>

                        <v-btn
                          color="danger darken-1"
                          text
                          @click="editProduct(eachProduct)"
                          outlined
                        >
                          Edit Product
                        </v-btn>
                      </v-card-actions>
                    </v-col>
                  </v-card>
                </v-dialog>

                <v-spacer></v-spacer>

                <v-dialog
                  v-model="buyProductDialog"
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
                        :src="selectedProduct.product_image.url"
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
                                {{ selectedProduct.product_name }}
                              </span>
                            </v-col>
                            <v-col cols="12">
                              <strong>Product Description</strong>
                              :
                              <span>
                                {{ selectedProduct.description }}
                              </span>
                            </v-col>

                            <v-col cols="12">
                              <h5>Purchase Details</h5>

                              <v-row>
                                <v-col cols="12">
                                  <v-text-field
                                    type="number"
                                    :value="selectedProduct.price"
                                    v-model="selectedProduct.price"
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
                          @click="buyProductDialog = false"
                          outlined
                        >
                          Close
                        </v-btn>

                        <v-btn color="success darken-1" text outlined>
                          <paystack
                            :amount="amount * 100"
                            :email="email"
                            :paystackkey="PUBLIC_KEY"
                            :reference="reference"
                            :callback="processPayment"
                            :close="close"
                          >
                            Pay with {{ paymentMethod.method }}
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
  </div>
</template>

<script lang="">
import axios from 'axios'
import paystack from 'vue-paystack'

export default {
  name: 'Product',
  components: {
    paystack,
  },
  data() {
    return {
      adminUsername: '',
      username: '',
      password: '',
      adminPassword: '',
      newProductAdminAuthDialog: false,
      editProductBoolean: false,
      productId: '',
      productSuccessfullyAdded: false,
      productAlreadyInCart: false,
      viewProductDetailsDialog: false,
      buyProductDialog: false,
      BASE_URL: '',
      PUBLIC_KEY: '',
      dialog: false,
      email: '',
      fullName: '',
      allProductsInCart: [],
      allAvailableProducts: [],
      selectedProduct: {},
      product_name: '',
      description: '',
      address: {
        location: '',
        postal_code: '',
        state: '',
        country: '',
      },
      product_details: {
        price: 1,
        quantity: 1,
        production_date: '',
        expiry_date: '',
      },
      product_image_details: {
        src: '',
        name: '',
        size: 0,
        type: '',
      },
      contact_info: {
        phone: '',
        email: '',
        website_url: '',
        website_title: '',
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
    }
  },

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
    //   // return this.message.split("").reverse().join("")
    //   return this.amount = this.quantityPurchased * this.selectedProduct.price
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
    this.username = this.$adminUsername
    this.password = this.$adminPassword
    // console.log(paystack)
    console.log(this.BASE_URL)
    console.log(this.$adminUsername)
    console.log(this.$adminPassword)

    axios
      .get(this.BASE_URL)
      .then((response) => {
        this.allAvailableProducts = response.data
        console.log(this.allAvailableProducts)
      })
      .catch((error) => {
        console.log(error)
      })

    this.selectedProduct = {
      product_name: this.product_name,
      description: this.description,
      address: this.address,
      product_details: this.product_details,
      contact_info: this.contact_info,
      product_category: this.product_category,
      product_image_details: this.product_image_details,
    }
  },

  methods: {
    adminAuth: () => {
      // const contact_info = {}
      console.log('test me')
      // let username  =  this.username
      // console.log(this.adminUsername)
      // if (this.adminUsername !== "Archyscript") {
      //   console.log('Admin Username is not correct')
      //   return
      // }
      console.log('test now')
      console.log(this.contact_info)
      // if (this.adminPassword !== this.password) {
      //   console.log('Admin password is not correct')
      //   return
      // }

      // this.newProductAdminAuthDialog = false

      // if (this.editProductBoolean) {
      //   return this.$router.push({ path: `/new-product/` })
      // } else {
      //   return this.$router.push({ path: `/new-product/add_new` })
      // }
    },
    resetValuesAndHideModalBox: () => {
      this.viewProductDetailsDialog = false
    },
    editProduct: (product) => {
      console.log(product)
      this.buyProductDialog = true
      this.newProductAdminAuthDialog = false
      this.viewProductDetailsDialog = false

      // if  (this.adminUsername !== this.$adminUsername) {
      //   console.log("Admin Username is not correct")
      //   return
      // }
      // if  (this.adminPassword !== this.$adminPassword) {
      //   console.log("Admin password is not correct")
      //  return
      // }

      // this.newProductAdminAuthDialog = false

      // if (this.editProductBoolean) {
      //   return this.$router.push({ path: `/new_product/` })
      // } else {
      //   return this.$router.push({ path: `/new_product/add_new` })
      // }
    },
    processPayment: () => {
      window.alert('Payment recieved')
      // this.$router.push({ path: `/home` })
    },
    close: () => {
      console.log('You closed checkout page')
    },
    calculateAmount() {
      return (this.amount = this.quantityPurchased * this.selectedProduct.price)
    },
    viewProductDetails(product) {
      // this.calculateAmount()
      // console.log(product)
      this.selectedProduct = product
      console.log(this.selectedProduct)
      // this.viewProductDetailsDialog = true
      // this.selectedProduct.product_name = product.product_name
      // this.selectedProduct.description = product.description
      // this.selectedProduct.price = product.product_details.price
      // this.selectedProduct.quantity =
      //   product.product_details.quantity
      // this.selectedProduct.product_image = product.product_image
    },
    buyProduct(product) {
      // this.dialog = true
      this.calculateAmount()
      console.log(this.selectedProduct)
      this.selectedProduct = product
      console.log(product)
      // this.selectedProduct.product_name = product.product_name
      // this.selectedProduct.description = product.description
      // this.selectedProduct.price = product.product_details.price
      // this.selectedProduct.quantity = product.product_details.quantity
      // this.selectedProduct.product_image = product.product_image
    },
    afterPaymentFunction() {
      this.selectedProduct = {
        product_id: '',
        product_image: '',
        product_name: '',
        product_description: '',
        price: 0,
        quantity: 1,
      }
    },
    proceedToMakePayment() {
      this.buyProductDialog = false
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
