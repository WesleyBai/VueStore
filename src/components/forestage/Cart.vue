<template>
  <div>
    <button
      class="btn btn-cart p-0"
      type="button"
      id="dropdownMenuButton"
      data-toggle="dropdown"
      data-offset="10,10"
      aria-haspopup="true"
      aria-expanded="false"
      @click.prevent="cartCar()"
    >
      <i class="fas fa-shopping-cart text-white fa-2x"></i>
      <span class="badge badge-pill badge-danger" v-if="navCartItem != 0">{{
        navCartItem
      }}</span>
    </button>

    <div
      class="dropdown-menu dropdown-menu-right border bg-dark text-white"
      style="min-width: 350px;"
      aria-labelledby="dropdownMenuButton"
    >
      <!-- 內容 -->
      <div class="container">
        <div class="my-4">
          <h6 class="text-center">已選擇的商品</h6>
          <table class="table text-white">
            <thead>
              <th>品名</th>
              <th>數量</th>
              <th>單價</th>
            </thead>
            <tbody>
              <tr v-for="item in navCart.carts" :key="item.id">
                <td class="align-middle">{{ item.product.title }}</td>
                <td class="align-middle">
                  {{ item.qty }}/{{ item.product.unit }}
                </td>
                <td class="align-middle text-right">
                  {{ item.final_total | currency }}
                </td>
              </tr>
            </tbody>
            <tfoot>
              <tr v-if="navCart.carts != ''">
                <td colspan="2" class="text-right">總金額</td>
                <td class="text-right">
                  {{ navCart.total | currency }}
                </td>
              </tr>
            </tfoot>
          </table>
          <p class="text-center h6" v-if="navCart.carts == ''">
            您還沒有選購任何商品
          </p>
          <div class="d-flex justify-content-end">
            <a
              href="#"
              class="btn btn-info"
              @click="payment()"
              v-if="navCart.carts != ''"
              >結帳</a
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import $ from 'jquery'

export default {
  props: [`navCart`, `navCartItem`],

  methods: {
    cartCar() {
      this.$emit('cartCar')
    },
    payment() {
      const vm = this
      vm.$router.push('/payment/order')
    }
  }
}
</script>
