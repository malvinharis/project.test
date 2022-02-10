<template>
  <!-- Voucher Payment Method -->
  <v-card class="voucher-payment__card" color="white">
    <!-- Voucher Checkout -->
    <div class="voucher-payment__head">
      <v-btn
        color="black"
        icon
        @click="
          (event) => {
            $emit('back', event)
          }
        "
      >
        <v-icon>mdi-chevron-left</v-icon>
      </v-btn>
      <div class="voucher-payment__title">Checkout</div>
    </div>
    <!-- Voucher Summary -->
    <div class="voucher-payment__summary">
      <div class="voucher-payment__summary-group">
        <div
          class="voucher-payment__summary-title light-green--text text--darken-2"
        >
          Total Amount
        </div>
        <div
          class="voucher-payment__summary-price light-green--text text--darken-2"
        >
          Rp.
          {{ formatPrice(parseInt(data.voucher.price) * data.form.quantity) }}
        </div>
      </div>
      <div
        class="voucher-payment__summary-subtitle light-green--text text--darken-1"
      >
        Your order {{ data.form.quantity }} item. Click to see details.
      </div>
    </div>
    <!-- Payment Methods -->
    <div
      v-for="(item, idx) in payments"
      :key="idx"
      class="voucher-payment__list"
    >
      <div class="voucher-payment__label">
        {{ item.type }}
      </div>
      <div
        v-for="(itemChild, idx2) in item.options"
        :key="idx2"
        class="voucher-payment__item"
        @click="handlePaymentMethod(item.type, itemChild.name)"
      >
        <div class="voucher-payment__item-logo">
          <v-img
            max-height="80"
            max-width="50"
            src="https://dummyimage.com/600x400/e3e3e3/fff&text=+"
          ></v-img>
        </div>
        <div class="voucher-payment__item-name">
          {{ itemChild.name }}
        </div>
        <v-icon large class="voucher-payment__item-icon">
          mdi-chevron-right
        </v-icon>
      </div>
    </div>
  </v-card>
</template>
<script>
export default {
  name: 'VoucherPaymentMethod',
  props: {
    data: Object,
  },
  data: () => ({
    selectedPayment: {
      type: '',
      name: '',
    },
    payments: [
      {
        type: 'e-Wallet',
        options: [
          {
            icon: '',
            name: 'Gopay',
          },
          {
            icon: '',
            name: 'OVO',
          },
          {
            icon: '',
            name: 'Dana',
          },
        ],
      },
      {
        type: 'Bank Transfer',
        options: [
          {
            icon: '',
            name: 'Bank BCA',
          },
          {
            icon: '',
            name: 'Bank BRI',
          },
          {
            icon: '',
            name: 'Bank BNI',
          },
          {
            icon: '',
            name: 'Bank Permata',
          },
          {
            icon: '',
            name: 'Bank Mandiri',
          },
        ],
      },
    ],
  }),
  methods: {
    formatPrice(value) {
      const val = (value / 1).toFixed(0).replace('.', ',')
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.')
    },
    handlePaymentMethod(value1, value2) {
      this.selectedPayment = {
        type: value1,
        name: value2,
      }
      this.$emit('payment-method', {
        data: this.selectedPayment,
        step: 'voucher-message',
      })
    },
  },
}
</script>
<style></style>
