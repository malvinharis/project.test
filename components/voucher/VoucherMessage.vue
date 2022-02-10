<template>
  <!-- Voucher Message -->
  <v-card class="voucher-message__card" color="light-green  darken-1">
    <!-- Voucher Message Head -->
    <div class="voucher-message__head">
      <v-btn
        color="white"
        icon
        @click="
          (event) => {
            $emit('exit', event)
          }
        "
      >
        <v-icon>mdi-close</v-icon>
      </v-btn>
    </div>
    <div class="voucher-message__text">Yay, Transaction Successfully !</div>

    <!-- Voucher Summary -->
    <div class="voucher-message__summary">
      <!-- Display Voucher -->
      <div class="voucher-message__summary-group">
        <div class="voucher-message__voucher">
          <div class="voucher-message__voucher-image">
            <v-img :src="data.voucher.image"></v-img>
          </div>
          <div class="voucher-message__voucher-group">
            <div class="voucher-message__voucher-title">
              {{ data.voucher.title }}
            </div>
            <div class="voucher-message__voucher-subtitle">
              {{ data.form.quantity }} Item
            </div>
          </div>
        </div>
      </div>
      <!-- Display Date & Status -->
      <div class="voucher-message__summary-group">
        <div class="voucher-message__item">
          <v-icon>mdi-calendar-month-outline</v-icon>
          <div class="voucher-message__item-content">24 Jan 2022 - 10:00</div>
        </div>
        <div class="voucher-message__item">
          <v-icon>mdi-file-document-outline</v-icon>
          <div
            class="voucher-message__item-content blue--text font-weight-medium"
          >
            On Process
          </div>
        </div>
      </div>
      <!-- Display Total Payment -->
      <div class="voucher-message__summary-group">
        <div class="voucher-message__payment">
          <div class="voucher-message__payment-title">Total Payment</div>
          <div
            class="voucher-message__payment-price orange--text text--accent-4"
          >
            Rp.
            {{ formatPrice(parseInt(data.voucher.price * data.form.quantity)) }}
          </div>
        </div>
      </div>
      <!-- Display Transaction -->
      <div class="voucher-message__summary-group">
        <div class="voucher-message__transaction">
          <div class="voucher-message__transaction-group">
            <div class="voucher-message__transaction-title">Transaction ID</div>
            <div class="voucher-message__transaction-subtitle">
              TADA-7791273
            </div>
          </div>
          <v-btn
            class="voucher-message__transaction-button"
            outlined
            color="orange accent-4"
            small
          >
            Copy
          </v-btn>
        </div>
      </div>
      <!-- Display Payment Detail -->
      <div class="voucher-message__summary-group">
        <div class="voucher-message__detail">
          <div class="voucher-message__detail-group">
            <div class="voucher-message__detail-title">Qty</div>
            <div class="voucher-message__detail-value">
              {{ data.form.quantity }}
            </div>
          </div>
          <div class="voucher-message__detail-group">
            <div class="voucher-message__detail-title">Amount</div>
            <div class="voucher-message__detail-value">
              Rp.
              {{ formatPrice(parseInt(data.voucher.price)) }}
            </div>
          </div>
        </div>
      </div>
      <!-- Display Merchant & Payment Method -->
      <div class="voucher-message__summary-group">
        <div class="voucher-message__detail">
          <div class="voucher-message__detail-group">
            <div class="voucher-message__detail-title">Merchant</div>
            <div class="voucher-message__detail-value">
              {{ data.method.type }}
            </div>
          </div>
          <div class="voucher-message__detail-group">
            <div class="voucher-message__detail-title">Payment Method</div>
            <div class="voucher-message__detail-value">
              {{ data.method.name }}
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="voucher-message__action">
      <v-btn
        block
        color="white"
        class="voucher-message__action-button white--text"
        large
        outlined
        @click="
          (event) => {
            $emit('exit', event)
          }
        "
      >
        Finish
      </v-btn>
    </div>
  </v-card>
</template>
<script>
export default {
  props: {
    data: Object,
  },
  methods: {
    formatPrice(value) {
      const val = (value / 1).toFixed(0).replace('.', ',')
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.')
    },
  },
}
</script>
<style lang=""></style>
