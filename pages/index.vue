<template>
  <div class="content">
    <div class="content__wrapper">
      <v-row justify="center">
        <!-- Headline -->
        <v-col cols="12" sm="8" md="4">
          <div class="headline">
            <div class="headline__head">
              <div class="headline__title">How it Works ?</div>
              <div class="headline__subtitle">
                Follow these steps to send a gift to your loved ones
              </div>
            </div>
            <div class="headline__body">
              <div class="headline__list">
                <div
                  v-for="(item, idx) in headlines"
                  :key="idx"
                  class="headline__item"
                >
                  <div class="headline__image"></div>
                  <div class="headline__content">
                    {{ item.content }}
                  </div>
                </div>
              </div>
            </div>
          </div>
        </v-col>
        <!-- Voucher Application Form -->
        <v-col cols="12" sm="8" md="4">
          <div class="voucher">
            <!-- Voucher List Component -->
            <template v-if="step === 'voucher-list'">
              <VoucherList
                :data="voucherGifts"
                @selected-voucher="handleStep"
              />
            </template>
            <!-- Voucher Form Component -->
            <template v-else-if="step === 'voucher-form'">
              <VoucherForm
                v-model="data"
                @form-done="handleStep"
                @back="handleBack"
              />
            </template>
            <!-- Voucher Payment Method Component-->
            <template v-else-if="step === 'payment-method'">
              <VoucherPaymentMethod :data="data" @back="handleBack" />
            </template>
            <!-- Voucher Message-->
            <template v-else-if="step === 'voucher-message'">
              <VoucherMessage :data="data" @exit="handleExit" />
            </template>
          </div>
        </v-col>
      </v-row>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data: () => ({
    step: 'voucher-list', // voucher-list -> voucher-form -> payment-method -> voucher-message
    headlines: [
      {
        content:
          '1. Select an available gift package. There are 3 types that you can choose from. All gift package, choose one package, and single gift.',
      },
      {
        content:
          "2. Fill in your data as well the recipient's data. Make sure the data has been filled in correctly",
      },
      {
        content:
          '3. Make a payment immediately through the available payment options',
      },
      {
        content:
          '4. Congratulations! You gift has been successfully sent to your loved ones',
      },
    ],
    voucherGifts: [
      {
        title: 'Home Living & Furniture Gift',
        type: 'Bundling',
        expDate: '20 Dec 2025',
        image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
        price: '3000000',
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
        price: '1000000',
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
        price: '30000000',
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
        ],
      },
      {
        title: 'Home Living Full Package Gift',
        type: 'Bundling',
        expDate: '30 Dec 2025',
        image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
        price: '50000000',
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
        price: '1000000',
        options: [],
      },
      {
        title: 'Gift Voucher 5.000.000',
        type: 'Single',
        expDate: '30 Dec 2025',
        image: 'https://dummyimage.com/600x400/ebebeb/fff&text=+',
        price: '5000000',
        options: [],
      },
    ],
    data: {
      voucher: {},
      form: {},
      method: {},
    },
  }),
  methods: {
    handleStep(e) {
      if (this.step === 'voucher-list') {
        this.data.voucher = e.data
        this.data.form = {
          type: 1,
          quantity: 1,
          method: ['email', 'whatsapp'],
          name: '',
          phoneNumber: '',
          recipientName: '',
          recipientWhatsapp: '',
          recipientEmail: '',
          message: '',
        }
        console.log(this.data)
      } else if (this.step === 'voucher-form') {
        this.data.form = e.data
      } else if (this.step === 'payment-method') {
        this.data.method = e.data
      }
      this.step = e.step
    },
    handleBack() {
      if (this.step === 'voucher-form') {
        this.step = 'voucher-list'
      } else if (this.step === 'payment-method') {
        this.step = 'voucher-form'
      }
    },
    handleExit() {
      this.step = 'voucher-list'
    },
  },
}
</script>
