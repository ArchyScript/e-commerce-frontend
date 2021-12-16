<template>
  <div>
    <v-container>
      <div>
        <h3>{{updateMode ? "Update Product Page" : "New Product Page"}}</h3>
      </div>

      <v-divider></v-divider>

      <v-form enctype="multipart/form-data">
        <v-row>
          <v-col cols="12">
            <v-row>
              <v-col cols="12">
                <h4>Basic Info</h4>
              </v-col>

              <v-col cols="12">
                <v-text-field
                  :value="product_name"
                  v-model="product_name"
                  label="Product Name"
                  outlined
                  filled
                ></v-text-field>
              </v-col>

              <v-col cols="12">
                <v-textarea
                  outlined
                  no-resize
                  rows="6"
                  label="Product Description"
                  v-model="description"
                  :value="description"
                  placeholder="Describe your product in details here..."
                  dense
                ></v-textarea>
              </v-col>
            </v-row>
          </v-col>

          <v-col cols="12">
            <v-row>
              <v-col cols="12">
                <h4>Address</h4>
              </v-col>

              <v-col cols="12" sm="6">
                <v-text-field
                  :value="address.location"
                  v-model="address.location"
                  label="Location"
                  outlined
                  disabled
                  filled
                ></v-text-field>
              </v-col>

              <v-col cols="12" sm="6">
                <v-text-field
                  :value="address.postal_code"
                  v-model="address.postal_code"
                  label="Postal Code"
                  outlined
                  disabled
                  filled
                ></v-text-field>
              </v-col>

              <v-col cols="12" sm="6">
                <v-text-field
                  :value="address.country"
                  v-model="address.country"
                  label="Country"
                  outlined
                  disabled
                  filled
                ></v-text-field>
              </v-col>

              <v-col cols="12" sm="6">
                <v-text-field
                  :value="address.state"
                  v-model="address.state"
                  label="State"
                  outlined
                  disabled
                  filled
                ></v-text-field>
              </v-col>
            </v-row>
          </v-col>

          <v-col cols="12">
            <v-row>
              <v-col cols="12">
                <h4>Product Details</h4>
              </v-col>

              <v-col cols="12" sm="6">
                <v-text-field
                  type="number"
                  :value="product_details.price"
                  v-model="product_details.price"
                  label="Price"
                  outlined
                  filled
                ></v-text-field>
              </v-col>

              <v-col cols="12" sm="6">
                <v-text-field
                  type="number"
                  :value="product_details.quantity"
                  v-model="product_details.quantity"
                  label="Quantity"
                  outlined
                  filled
                ></v-text-field>
              </v-col>

              <v-col cols="12" sm="6">
                <v-menu
                  ref="production_date_menu"
                  v-model="production_date_menu"
                  :close-on-content-click="false"
                  transition="scale-transition"
                  offset-y
                  max-width="290px"
                  min-width="auto"
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-text-field
                      v-model="product_details.production_date"
                      label="Production Date"
                      append-icon="mdi-calendar"
                      outlined
                      readonly
                      v-bind="attrs"
                      v-on="on"
                    ></v-text-field>
                  </template>
                  <v-date-picker
                    v-model="product_details.production_date"
                    no-title
                    scrollable
                  >
                    <v-spacer></v-spacer>
                    <v-btn
                      text
                      color="danger"
                      @click="production_date_menu = false"
                    >
                      Cancel
                    </v-btn>
                    <v-btn
                      text
                      color="success"
                      @click="
                        $refs.production_date_menu.save(
                          product_details.production_date,
                        )
                      "
                    >
                      OK
                    </v-btn>
                  </v-date-picker>
                </v-menu>
              </v-col>

              <v-col cols="12" sm="6">
                <v-menu
                  ref="expiry_date_menu"
                  v-model="expiry_date_menu"
                  :close-on-content-click="false"
                  transition="scale-transition"
                  offset-y
                  max-width="290px"
                  min-width="auto"
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-text-field
                      v-model="product_details.expiry_date"
                      label="Production Date"
                      append-icon="mdi-calendar"
                      outlined
                      readonly
                      v-bind="attrs"
                      v-on="on"
                    ></v-text-field>
                  </template>
                  <v-date-picker
                    v-model="product_details.expiry_date"
                    no-title
                    scrollable
                  >
                    <v-spacer></v-spacer>
                    <v-btn
                      text
                      color="danger"
                      @click="expiry_date_menu = false"
                    >
                      Cancel
                    </v-btn>
                    <v-btn
                      text
                      color="success"
                      @click="
                        $refs.expiry_date_menu.save(product_details.expiry_date)
                      "
                    >
                      OK
                    </v-btn>
                  </v-date-picker>
                </v-menu>
              </v-col>
            </v-row>
          </v-col>

          <v-col cols="12">
            <v-row>
              <v-col cols="12">
                <h4>Contact Info</h4>
              </v-col>

              <v-col cols="12" sm="6">
                <v-text-field
                  type="number"
                  :value="contact_info.phone"
                  v-model="contact_info.phone"
                  label="Phone"
                  outlined
                  filled
                ></v-text-field>
              </v-col>

              <v-col cols="12" sm="6">
                <v-text-field
                  type="email"
                  :value="contact_info.email"
                  v-model="contact_info.email"
                  :rules="emailRules"
                  label="Email"
                  outlined
                  filled
                ></v-text-field>
              </v-col>

              <v-col cols="12" sm="6">
                <v-text-field
                  type="text"
                  :value="contact_info.website_url"
                  v-model="contact_info.website_url"
                  label="Website URL"
                  placeholder="e.g https://citonhub.com"
                  hint="'https://citonhub.com' will be the default url if it is empty"
                  persistent-hint
                  disabled
                  outlined
                  filled
                ></v-text-field>
              </v-col>

              <v-col cols="12" sm="6">
                <v-text-field
                  type="text"
                  :value="contact_info.website_title"
                  v-model="contact_info.website_title"
                  label="Website Title"
                  placeholder="e.g CitonHub"
                  hint="'CitonHub' will be the default title if it is empty"
                  disabled
                  persistent-hint
                  outlined
                  filled
                ></v-text-field>
              </v-col>
            </v-row>
          </v-col>

          <v-col cols="12">
            <v-row>
              <v-col cols="12">
                <h4>Category</h4>
              </v-col>

              <v-col ccols="12" sm="6">
                <v-select
                  v-model="product_category"
                  :hint="`${product_category.category}, ${product_category.type}`"
                  :items="categories"
                  outlined
                  append-icon="mdi-map"
                  item-text="category"
                  item-value="category"
                  hide-details
                  label="select product category"
                  return-object
                  single-line
                ></v-select>
              </v-col>
            </v-row>
          </v-col>

          <!-- <v-col cols="12">
            <v-text-field
              :value="product_name"
              v-model="product_name"
              label="Product Name"
              outlined
              filled
            ></v-text-field>
          </v-col>

          <v-col cols="12">
            <v-textarea
              :rules="[rules.required, rules.length(250)]"
              outlined
              no-resize
              rows="6"
              label="Product Description"
              v-model="description"
              :value="description"
              placeholder="Describe your product in details here..."
              dense
            ></v-textarea>
          </v-col> -->

          <!-- <v-col ccols="12" sm="6">
            <v-rating v-model="rating">
              <template v-slot:item="props">
                <v-icon
                  :color="
                    props.isFilled ? genColor(props.index) : 'grey lighten-1'
                  "
                  large
                  @click="props.click"
                >
                  {{
                    props.isFilled
                      ? 'mdi-star-circle'
                      : 'mdi-star-circle-outline'
                  }}
                </v-icon>
              </template>
            </v-rating>
          </v-col> -->
          <!-- <v-col cols="12" sm="6">
            <v-text-field
              :value="product_category.type"
              label="Continent"
              filled
              disabled
              outlined
              readonly
            ></v-text-field>
          </v-col> -->

          <!-- <v-col cols="12" sm="6">
            <v-checkbox
              v-model="stillExist"
              label="Does building STILL exist?"
            ></v-checkbox>
          </v-col> -->

          <!-- <v-col>
          <span> Contact Information </span>
        </v-col> -->

          <!-- <v-col cols="12" sm="6">
            <v-file-input
              label="Add Picture"
              @change="selectFile"
              ref="fileInput"
              outlined
            ></v-file-input>
          </v-col> -->
          <v-col cols="6">
            <v-img
              :src="product_image_details.src"
              :lazy-src="product_image_details.src"
              max-width="300"
              max-height="300"
              rounded
              outlined
              class="mx-auto mb-5"
            >
              <template v-slot:placeholder>
                <v-row class="fill-height ma-0" align="center" justify="center">
                  <v-progress-circular
                    indeterminate
                    color="grey lighten-5"
                  ></v-progress-circular>
                </v-row>
              </template>
            </v-img>

            <input
              ref="fileInput"
              class="d-none"
              type="file"
              accept="image/*"
              @change="selectFile"
            />
            <v-btn
              color="primary"
              cols="6"
              outlined
              block
              dark
              :loading="isSelecting"
              @click="handleFileImport"
            >
              Choose a file
            </v-btn>
          </v-col>

          <v-col cols="12" class="text-center mt-15">
            <v-btn outlined block class="ma-2" @click="getAll">
              Get All Request
              <v-icon right>mdi-map</v-icon>
            </v-btn>
            <v-btn outlined block class="ma-2" @click="getSingleProduct">
              Get Single Product
              <v-icon right>mdi-map</v-icon>
            </v-btn>
            <v-btn outlined block class="ma-2" @click="editSingle">
              Edit Single
              <v-icon right>mdi-map</v-icon>
            </v-btn>
            <v-btn outlined block class="ma-2" @click="updateSingle">
              Update Product
              <v-icon right>mdi-map</v-icon>
            </v-btn>
            <v-btn outlined block class="ma-2" @click="deleteSingle">
              Delete Product
              <v-icon right>mdi-map</v-icon>
            </v-btn>
            <v-btn outlined block class="ma-2" @click="uploadProduct">
              {{updateMode ? "Update Product" : "Add New Product"}} 
              <v-icon right>mdi-map</v-icon>
            </v-btn>
          </v-col>
        </v-row>
      </v-form>
    </v-container>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'NewProduct',
  data: () => ({
    // BASE_URL: 'localhost:5000/api/products',
    BASE_URL: "",
    input_file: '',
    product_image_src: '',
    product_name: '',
    description: '',
    updateMode: false,
    preview_image_boolean: true,
    address: {
      location: 'Test 2 location',
      postal_code: 'DQDW3X4PF',
      state: 'Lagos',
      country: 'Nigeria',
    },
    product_details: {
      price: 1,
      quantity: 1,
      production_date: new Date(
        Date.now() - new Date().getTimezoneOffset() * 60000,
      )
        .toISOString()
        .substr(0, 10),
      expiry_date: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10),
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
      website_url: 'https://citonhub.com',
      website_title: 'CitonHub',
    },
    isSelecting: false,
    selectedFile: null,
    product_id: '61ac9c1f9422b18af813901a',
    allRequest: [],
    sele: {},
    product_category: { category: 'Lifestyle', type: 'clothing' },
    production_date_menu: false,
    expiry_date_menu: false,
    rules: {
      length: (len) => (v) =>
        (v || '').length >= len || `Invalid character length, required ${len}`,
      required: (v) => !!v || 'This field is required',
    },
    emailRules: [
      (v) => !!v || 'E-mail is required',
      (v) => /.+@.+\..+/.test(v) || 'E-mail must be valid',
    ],
    categories: [
      { category: 'Florida', type: 'FL' },
      { category: 'Georgia', type: 'GA' },
      { category: 'Nebraska', type: 'NE' },
      { category: 'California', type: 'CA' },
      { category: 'Trst', type: 'GA' },
      { category: 'ddeas', type: 'GA' },
      { category: 'wregred', type: 'NE' },
      { category: 'rtredsx', type: 'CA' },
      { category: 'efwwe23ras', type: 'GA' },
    ],
  }),
  methods: {
    handleFileImport() {
      this.isSelecting = true
      // After obtaining the focus when closing the FilePicker, return the button state to normal
      window.addEventListener(
        'focus',
        () => {
          this.isSelecting = false
        },
        { once: true },
      )
      // Trigger click on the FileInput
      this.$refs.fileInput.click()
    },
    selectFile(event) {
      if (event.target.files.length < 1)
        return console.log('Please select an image for upload')

      // Trigger click on the FileInput
      this.selectedFile = event.target.files[0]

      var image_src = URL.createObjectURL(this.selectedFile)
      this.product_image_details.src = image_src
      this.preview_image_boolean = true

      this.product_image_details = {
        src: image_src,
        name: this.selectedFile.name,
        size: this.selectedFile.size,
        type: this.selectedFile.type,
      }
      console.log(this.product_image_details)
      // }

      // this.selectedFile = event.target.files[0]
      // console.log(file)
      // console.log(event)

      // console.log(this.input_file)
      // axios.post('my-domain.com/file-upload', this.selectedFile)
      // const formData = new FormData()
      // formData.append('myFile', this.selectedFile, this.selectedFile.name)
      // axios.post('my-domain.com/file-upload', formData, {
      //   onUploadProgress: (progressEvent) => {
      //     console.log(progressEvent.loaded / progressEvent.total)
      //   },
      // })
    },
    genColor(i) {
      return this.colors[i]
    },
    uploadProduct() {
      const product = {
        product_name: this.product_name,
        description: this.description,
        address: this.address,
        product_details: this.product_details,
        contact_info: this.contact_info,
        product_category: this.product_category,
        product_image_details: this.product_image_details,
      }

      axios
        .post(`${this.BASE_URL}`, product)
        .then((response) => {
          console.log(response)
        })
        .catch((error) => {
          console.log(error)
        })
    },

    getSingleProduct() {
      const product_id = this.product_id
      axios
        .get(`${this.BASE_URL}/${product_id}`)
        .then((response) => {
          console.log(response.data)
        })
        .catch((error) => {
          console.log(error)
        })
    },

    editSingle() {
      const product_id = this.product_id

      axios
        .get(`${this.BASE_URL}/${product_id}`)
        .then((response) => {
          this.preview_image_boolean = true

          this.product_name = response.data.product_name
          this.description = response.data.description
          this.address = response.data.address
          this.product_details = response.data.product_details
          this.contact_info = response.data.contact_info
          this.product_category = response.data.product_category
          this.product_image_details = response.data.product_image_details
        })
        .catch((error) => {
          console.log(error)
        })
    },

    deleteSingle() {
      axios
        .delete(`${this.BASE_URL}/${this.product_id}`)
        .then((response) => {
          console.log(response.data)
        })
        .catch((error) => {
          console.log(error)
        })
    },

    updateSingle() {
      const productUpdateData = {
        product_name: this.product_name,
        description: this.description,
        address: this.address,
        product_details: this.product_details,
        contact_info: this.contact_info,
        product_category: this.product_category,
        product_image_details: this.product_image_details,
      }
      axios
        .patch(`${this.BASE_URL}/${this.product_id}`, productUpdateData)
        .then((response) => {
          console.log(response.data)
        })
        .catch((error) => {
          console.log(error)
        })
    },

    getAll() {
      axios
        .get(this.BASE_URL)
        .then((response) => {
          console.log(response.data)
        })
        .catch((error) => {
          console.log(error)
        })
    },
  },
  created() {
    this.BASE_URL = this.$BASE_URL
    console.log(this.BASE_URL)

    console.log(this.$router.params.product_id)
    if (this.$router.params.product_id) {
      this.updateMode = true
    } else {
      this.updateMode = false
    }

    console.log(this.$appName)
  },
}
</script>

<style lang="css">
.preview img {
  width: 100%;
  display: none;
  margin-top: 10px;
}
</style>
