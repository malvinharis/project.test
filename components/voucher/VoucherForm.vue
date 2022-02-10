<template>
  <!-- Voucher Form -->
  <v-card class="voucher-form__card" color="grey lighten-5">
    <!-- Voucher Cover -->
    <div class="voucher__display">
      <v-img
        class="voucher__image white--text"
        height="200px"
        :src="data.voucher.image"
      >
        <v-app-bar flat color="rgba(0, 0, 0, 0)">
          <v-btn
            color="white"
            icon
            @click="
              (event) => {
                $emit('back', event)
              }
            "
          >
            <v-icon>mdi-chevron-left</v-icon>
          </v-btn>
        </v-app-bar>
      </v-img>
      <div class="voucher__information pa-4">
        <div class="voucher__date grey--text lighten-4">
          Exp. {{ data.voucher.expDate }}
        </div>
        <div class="voucher__title">{{ data.voucher.title }}</div>
        <div class="voucher__price orange--text text--accent-4">
          Rp. {{ formatPrice(parseInt(data.voucher.price)) }}
        </div>
      </div>
    </div>

    <!-- Voucher Gift Options -->
    <div v-if="data.voucher.options.length" class="voucher__options">
      <div class="voucher__options-headline">
        The recipent can choose one of these gift options
      </div>
      <div class="voucher__options-list">
        <v-row justify="center" align="center">
          <v-col
            v-for="(item, idx) in data.voucher.options"
            :key="idx"
            cols="12"
            sm="12"
            md="6"
          >
            <div class="voucher__options-item">
              <v-img class="voucher__options-image" :src="item.image"></v-img>
              <div class="voucher__options-title">
                {{ item.title }}
              </div>
            </div>
          </v-col>
        </v-row>
      </div>
    </div>

    <!-- Voucher Gift Form Input -->
    <v-form ref="form" v-model="valid" lazy-validation class="voucher-form">
      <!-- Voucher Type -->
      <div class="voucher-form__group">
        <div class="voucher-form__title">Select Voucher Type</div>
        <div class="voucher-form__subtitle">
          Select the type of voucher you want to buy
        </div>
        <v-row justify="start" class="pt-2">
          <v-col v-for="(item, idx) in voucherTypes" :key="idx" md="auto">
            <v-btn
              class="voucher-form__button-type"
              :class="
                form.type === item.value ? 'orange--text text--accent-4' : ''
              "
              rounded
              outlined
              @click="form.type = item.value"
            >
              {{ item.label }}
            </v-btn>
          </v-col>
        </v-row>
      </div>

      <!-- Voucher Quantity -->
      <div class="voucher-form__group">
        <div class="voucher-form__quantity-group">
          <div class="voucher-form__title">Quantity</div>
          <div class="voucher-form__quantity">
            <v-btn
              class="voucher-form__quantity-button"
              elevation="0"
              dense
              @click="form.quantity >= 2 ? form.quantity-- : false"
            >
              -
            </v-btn>
            <v-text-field
              v-model.number="form.quantity"
              class="voucher-form__quantity-input"
              type="number"
              dense
              required
              outlined
              hide-details
            ></v-text-field>
            <v-btn
              class="voucher-form__quantity-button"
              elevation="0"
              dense
              @click="form.quantity++"
            >
              +
            </v-btn>
          </div>
        </div>
      </div>

      <!-- Voucher Delivery Method -->
      <div class="voucher-form__group">
        <div class="voucher-form__title">Delivery Method</div>
        <div class="voucher-form__subtitle">
          Select the method how to send the voucher
        </div>
        <v-row justify="start" class="py-3">
          <v-col
            v-for="(item, idx) in voucherMethod"
            :key="idx"
            cols="12"
            class="py-0"
          >
            <v-checkbox
              v-model="form.method"
              :rules="[rules.input.required]"
              class="voucher-form__checkbox"
              :label="item.label"
              :value="item.value"
              hide-details
              hide-spin-buttons
              dense
              color="orange accent-4"
              required
            ></v-checkbox>
          </v-col>
        </v-row>
      </div>

      <!-- Voucher Personoal Info -->
      <div class="voucher-form__group">
        <div class="voucher-form__title">Personal Info</div>
        <v-row justify="start" class="pt-6">
          <v-col cols="12">
            <v-text-field
              v-model="form.name"
              :rules="[rules.input.required]"
              class="voucher-form__input"
              label="Your Name"
              placeholder="E.g.: Saputra"
              required
              outlined
              hide-details
            ></v-text-field>
          </v-col>
          <v-col cols="12">
            <v-text-field
              v-model.number="form.phoneNumber"
              :rules="[rules.input.required]"
              class="voucher-form__input"
              type="number"
              label="Phone Number"
              placeholder="E.g.: 081234567890"
              required
              outlined
              hide-details
            ></v-text-field>
          </v-col>
        </v-row>
      </div>

      <!-- Voucher Recipient Info -->
      <div class="voucher-form__group">
        <div class="voucher-form__title">Recipient Info</div>
        <v-row justify="start" class="pt-6">
          <v-col cols="12">
            <v-text-field
              v-model="form.recipientName"
              :rules="[rules.input.required]"
              class="voucher-form__input"
              label="Recipient Name"
              placeholder="E.g.: Natasha Putri"
              required
              outlined
              hide-details
            ></v-text-field>
          </v-col>
          <v-col cols="12">
            <v-text-field
              v-model.number="form.recipientWhatsapp"
              :rules="[rules.input.required]"
              class="voucher-form__input"
              type="number"
              label="Whatsapp Recipient"
              placeholder="E.g.: 081234567890"
              required
              outlined
              hide-details
            ></v-text-field>
          </v-col>
          <v-col cols="12">
            <v-text-field
              v-model="form.recipientEmail"
              class="voucher-form__input"
              label="Email Address Recipient"
              placeholder="E.g.: recipient_name@gmail.com"
              :rules="[rules.email.required, rules.email.format]"
              required
              outlined
              hide-details
            ></v-text-field>
          </v-col>

          <v-col cols="12">
            <div class="voucher-form__input-title">Message</div>
            <div class="voucher-form__input-subtitle">
              Customize your message with 500 characters or less to make the
              recipient(s) smile
            </div>
            <v-textarea
              v-model="form.message"
              :rules="[rules.input.required, rules.message.max]"
              class="voucher-form__input pt-4"
              rows="3"
              counter="500"
              outlined
            ></v-textarea>
          </v-col>
        </v-row>
      </div>

      <!-- Voucher Term and Condition -->
      <div class="voucher-form__group">
        <div class="voucher-form__title">Term & Condition</div>
        <ul class="voucher-form__description">
          <li
            v-for="(item, idx) in voucherTermsAndCondition"
            :key="idx"
            class="voucher-form__description-item"
          >
            {{ item }}
          </li>
        </ul>
        <v-btn
          class="voucher-form__button-more"
          outlined
          color="orange accent-4"
          small
        >
          See All
        </v-btn>
      </div>

      <!-- Voucher Action -->
      <div class="voucher-form__group voucher-form__action">
        <v-btn
          :disabled="!valid"
          block
          color="orange accent-4"
          class="voucher-form__action-button white--text"
          large
          @click="validate"
        >
          Buy Now Rp.
          {{ formatPrice(parseInt(data.voucher.price) * form.quantity) }}
          <v-icon right> mdi-arrow-right </v-icon>
        </v-btn>
      </div>
    </v-form>
  </v-card>
</template>
<script>
export default {
  name: 'VoucherForm',
  props: {
    value: {
      type: Object,
    },
  },
  data: () => ({
    valid: true,
    summary: {
      form: {},
    },
    rules: {
      input: {
        required: (v) => !!v || 'Input is required',
      },
      message: {
        max: (v) =>
          v.length <= 500 || 'The max length of 500 characters is reached',
      },
      email: {
        required: (v) => !!v || 'E-mail is required',
        format: (v) =>
          /.+@.+\..+/.test(v) ||
          'Email must contain “@” and ”.” in the right places',
      },
    },
    voucherGifts: [
      {
        title: 'Home Living & Furniture Gift',
        type: 'Bundling',
        expDate: '20 Dec 2025',
        image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
        price: '3.000.000',
        options: [
          {
            title: 'Montreal Teal Velvet Sofa',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Meja Tamu Walnut',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Gallio Rak Dinding',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Standing Pot - 10 Pcs',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Kursi Braga - 2 Pcs',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Gift Voucher Rp 3.000.000',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
        ],
      },
      {
        title: 'Special Gift Electronic',
        type: 'Bundling',
        expDate: '30 Dec 2025',
        image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
        price: '1.000.000',
        options: [
          {
            title: 'Montreal Teal Velvet Sofa',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Meja Tamu Walnut',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Gallio Rak Dinding',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Standing Pot - 10 Pcs',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Kursi Braga - 2 Pcs',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Gift Voucher Rp 3.000.000',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
        ],
      },
      {
        title: 'Awesome Gadget Full Package Gift',
        type: 'Bundling',
        expDate: '30 Dec 2025',
        image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
        price: '30.000.000',
        options: [
          {
            title: 'Montreal Teal Velvet Sofa',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Meja Tamu Walnut',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Gallio Rak Dinding',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Standing Pot - 10 Pcs',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Kursi Braga - 2 Pcs',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Gift Voucher Rp 3.000.000',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
        ],
      },
      {
        title: 'Home Living Full Package Gift',
        type: 'Bundling',
        expDate: '30 Dec 2025',
        image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
        price: '50.000.000',
        options: [
          {
            title: 'Montreal Teal Velvet Sofa',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Meja Tamu Walnut',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Gallio Rak Dinding',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Standing Pot - 10 Pcs',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Kursi Braga - 2 Pcs',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
          {
            title: 'Gift Voucher Rp 3.000.000',
            image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
          },
        ],
      },
      {
        title: 'Gift Voucher 1.000.000',
        type: 'Single',
        expDate: '30 Dec 2025',
        image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
        price: '1.000.000',
        options: [],
      },
      {
        title: 'Gift Voucher 5.000.000',
        type: 'Single',
        expDate: '30 Dec 2025',
        image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
        price: '5.000.000',
        options: [],
      },
    ],
    voucherTypes: [
      {
        label: 'Buy for my self',
        value: 1,
      },
      {
        label: 'Send for Someone else',
        value: 2,
      },
    ],
    voucherMethod: [
      {
        label: 'Email',
        value: 'email',
      },
      {
        label: 'Whatsapp',
        value: 'whatsapp',
      },
    ],
    voucherTermsAndCondition: [
      'The Recipient can choose one of these gift options',
      'Voucher that have been received cannot be returned or exchanged for other vouchers',
      'Vouchers can be used until the expiration date stated on the voucher',
    ],
  }),
  computed: {
    form() {
      return this.value.form
    },
  },
  async created() {
    await this.fetchData()
  },
  methods: {
    fetchData() {
      this.data = this.value
    },
    formatPrice(value) {
      const val = (value / 1).toFixed(0).replace('.', ',')
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.')
    },
    validate() {
      const valid = this.$refs.form.validate()
      if (valid) {
        this.handleSubmitForm()
      }
    },
    async handleSubmitForm() {
      try {
        this.summary.form = await this.form
      } catch (error) {
        // Error
        console.error(error)
      } finally {
        this.$emit('form-done', {
          data: this.summary.form,
          step: 'payment-method',
        })
      }
    },
  },
}
</script>
<style></style>
