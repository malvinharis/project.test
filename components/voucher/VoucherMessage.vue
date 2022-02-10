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
            $emit('back', event)
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
            <v-img
              src="https://dummyimage.com/600x400/e3e3e3/fff&text=+"
            ></v-img>
          </div>
          <div class="voucher-message__voucher-group">
            <div class="voucher-message__voucher-title">Home Living</div>
            <div class="voucher-message__voucher-subtitle">1 Item</div>
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
            Rp. 3.000.000
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
            <div class="voucher-message__detail-value">1</div>
          </div>
          <div class="voucher-message__detail-group">
            <div class="voucher-message__detail-title">Amount</div>
            <div class="voucher-message__detail-value">Rp. 3.000.000</div>
          </div>
        </div>
      </div>
      <!-- Display Merchant & Payment Method -->
      <div class="voucher-message__summary-group">
        <div class="voucher-message__detail">
          <div class="voucher-message__detail-group">
            <div class="voucher-message__detail-title">Merchant</div>
            <div class="voucher-message__detail-value">My Brand</div>
          </div>
          <div class="voucher-message__detail-group">
            <div class="voucher-message__detail-title">Payment Method</div>
            <div class="voucher-message__detail-value">Bank BCA</div>
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
      >
        Finish
      </v-btn>
    </div>
  </v-card>
</template>
<script>
export default {}
</script>
<style lang=""></style>
