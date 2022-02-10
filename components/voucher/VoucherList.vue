<template>
  <!-- Voucher Gift -->
  <v-card class="voucher-gift">
    <v-img
      class="voucher-gift__banner white--text align-end"
      height="200px"
      src="https://dummyimage.com/600x400/d38434/ffffff&text=+"
    >
      <v-card-title>Gift Voucher</v-card-title>
    </v-img>

    <v-card-text class="voucher-gift__content">
      <!-- Voucher Gift List -->
      <div class="voucher-gift__list">
        <v-row justify="center" align="center">
          <v-col
            v-for="(item, idx) in data"
            :key="idx"
            cols="12"
            sm="12"
            md="6"
          >
            <v-card
              class="voucher-gift__item"
              elevation="1"
              @click="selectVoucher(item)"
            >
              <v-img
                class="voucher-gift__item-banner"
                height="150px"
                :src="item.image"
              >
                <v-app-bar
                  v-if="item.options.length"
                  flat
                  color="rgba(0, 0, 0, 0)"
                >
                  <v-spacer />
                  <v-chip color="blue" class="white--text">
                    {{ item.options.length }} Voucher
                  </v-chip>
                </v-app-bar>
              </v-img>

              <v-card-text class="voucher-gift__item-content">
                <div class="voucher__information p-4">
                  <div class="voucher__date">
                    {{ item.expDate }}
                  </div>
                  <div class="voucher__title">
                    {{ item.title }}
                  </div>
                  <div class="voucher__price orange--text text--accent-4">
                    Rp. {{ formatPrice(parseInt(item.price)) }}
                  </div>
                </div>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </div>
    </v-card-text>
  </v-card>
</template>
<script>
export default {
  name: 'VoucherList',
  props: {
    data: Array,
  },
  data: () => ({}),
  methods: {
    formatPrice(value) {
      const val = (value / 1).toFixed(0).replace('.', ',')
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.')
    },
    selectVoucher(item) {
      this.$emit('selected-voucher', { data: item, step: 'voucher-form' })
    },
  },
}
</script>
<style></style>
