<template>
  <div>
    <loading :active.sync="isLoading"></loading>
    <Navbar />
    <div class="container py-5">
      <div class="h1 text-center mb-5">紳士衣櫥</div>
      <div class="form-row text-center mb-5 text-white">
        <div class="col-md">
          <div class="alert alert-active rounded-pill">1.確認商品內容</div>
        </div>
        <div class="col-md">
          <div class="alert alert-disable rounded-pill">2.填寫個人資料</div>
        </div>
        <div class="col-md">
          <div class="alert alert-disable rounded-pill">3.完成訂單</div>
        </div>
      </div>

      <div class="row justify-content-center">
        <div class="col-md-8 border p-3">
          <div class="h3 text-center py-3">購物車資訊</div>
          <div class="mb-4 border-0">
            <div
              class="card-header d-flex justify-content-end align-items-end border-0"
              style="background-color: #181a1b;"
              v-if="cart.carts != ''"
            >
              <button
                class="btn text-white"
                type="button"
                data-toggle="collapse"
                data-target="#collapseOne"
                aria-expanded="true"
                aria-controls="collapseOne"
              >
                <span>
                  購物車內容
                  <i class="fas fa-angle-down"></i>
                </span>
              </button>
              <span
                class="ml-auto mb-0 h2"
                v-if="cart.final_total == cart.total"
                >{{ cart.total | currency }}</span
              >
              <span
                class="ml-auto mb-0 h2"
                v-if="cart.final_total !== cart.total"
                >{{ cart.final_total | currency }}</span
              >
            </div>
            <div class="text-center pt-4 h5" v-if="cart.carts == ''">
              購物車目前無任何商品
              <div class="pt-4">
                <router-link
                  class="btn btn-link text-decoration-none"
                  to="/shop"
                  >繼續選購商品</router-link
                >
              </div>
            </div>
          </div>
          <div
            id="collapseOne"
            class="collapse show"
            aria-labelledby="headingOne"
            v-if="cart.carts != ''"
          >
            <table class="table text-white">
              <thead>
                <th width="30"></th>
                <th width="100"></th>
                <th>商品名稱</th>
                <th width="110" class="w-sm">數量</th>
                <th width="110" class="w-sm">小計</th>
              </thead>
              <tbody>
                <tr v-for="item in cart.carts" :key="item.id">
                  <td class="align-middle">
                    <button
                      type="button"
                      class="btn btn-outline-danger btn-sm"
                      data-target="#removeCart"
                      data-toggle="modal"
                    >
                      <i class="far fa-trash-alt"></i>
                    </button>
                  </td>
                  <td>
                    <img
                      :src="item.product.imageUrl"
                      class="w-100 p-1 border"
                    />
                  </td>
                  <td class="align-middle">{{ item.product.title }}</td>
                  <td class="align-middle">
                    {{ item.qty }}/{{ item.product.unit }}
                  </td>
                  <td class="align-middle text-right">
                    {{ item.final_total | currency }}
                  </td>
                  <!-- 透過vm.cart中的carts帶入後端資料 -->

                  <!-- 刪除提示Modal -->
                  <div
                    class="modal fade"
                    id="removeCart"
                    tabindex="-1"
                    role="dialog"
                    aria-labelledby="removeCartLabel"
                    aria-hidden="true"
                  >
                    <div
                      class="modal-dialog modal-dialog-centered"
                      role="document"
                    >
                      <div
                        class="modal-content bg-dark   border border-secondary"
                      >
                        <div class="modal-body text-center p-4 h4">
                          你確定要移除這項商品嗎
                        </div>

                        <div
                          class="row text-center  border-top border-secondary m-0"
                        >
                          <div
                            data-dismiss="modal"
                            class="col-6 p-0 btn btn-outline-danger border-0"
                          >
                            <div class="p-2 border-right border-secondary">
                              取消
                            </div>
                          </div>

                          <div
                            class="col-6 p-0 btn btn-outline-danger border-0"
                          >
                            <div
                              class="p-2"
                              @click.prevent="removeCartItem(item.id)"
                            >
                              確定
                              <!-- removeCartItem(item.id) 按下按鈕移除單一筆資料 -->
                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </tr>
              </tbody>
              <tfoot>
                <tr v-if="cart.final_total == cart.total">
                  <td colspan="4" class="text-right">總金額</td>
                  <td class="text-right">{{ cart.total | currency }}</td>
                </tr>

                <tr v-if="cart.final_total !== cart.total">
                  <!-- 加上則扣後最終金額不等於原始總金額時才會顯示 -->
                  <td colspan="3" class="text-success text-left">
                    已套用優惠券
                  </td>
                  <td class="text-success">折扣後金額</td>
                  <td class="text-right text-success">
                    {{ cart.final_total | currency }}
                  </td>
                </tr>
              </tfoot>
            </table>
            <div class="input-group mb-3 input-group-sm">
              <input
                type="text"
                class="form-control input-color"
                v-model="coupon_code"
                placeholder="請輸入優惠碼"
              />
              <!--在後端資料庫中抓取與v-model相同的文字做為比對-->
              <div class="input-group-append">
                <button
                  class="btn btn-outline-secondary btn-w text-white"
                  type="button"
                  @click="addCouponCode"
                >
                  <!--addCouponCode 比對成功時將可帶入折扣-->
                  套用優惠碼
                </button>
                <div
                  class="d-flex align-self-center ml-2  animated js-flash infinite"
                >
                  <i
                    class="far fa-question-circle text-warning"
                    data-toggle="tooltip"
                    data-placement="right"
                    data-html="true"
                    title="<p>優惠期間：</p><p>輸入vip - 75折</p><p>輸入vvip - 5折</p>"
                  >
                  </i>
                </div>
              </div>
            </div>
          </div>

          <div class="text-right" v-if="cart.carts != ''">
            <router-link class="btn btn-info" to="/shop">繼續選購</router-link>
            <a href="#" class="btn btn-info ml-2" @click="goForm">前往付款</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import $ from 'jquery'
import Navbar from '@/components/forestage/Navbar'

export default {
  data() {
    return {
      cart: [],
      isLoading: false,
      coupon_code: '',
      products: []
    }
  },
  methods: {
    getCart() {
      const vm = this
      const api = `${process.env.VUE_APP_APIPATH}/api/${process.env.VUE_APP_CUSTOMPATH}/cart`
      vm.isLoading = true
      this.$http.get(api).then(response => {
        vm.cart = response.data.data

        // console.log('購物車資料', response.data)
        vm.isLoading = false
      })
    },
    removeCartItem(id) {
      const vm = this
      const api = `${process.env.VUE_APP_APIPATH}/api/${process.env.VUE_APP_CUSTOMPATH}/cart/${id}`

      this.$http.delete(api).then(response => {
        vm.getCart()

        $('#removeCart').modal('hide')
        this.$bus.$emit('message:push', '商品已被刪除', 'yellow')
      })
    },
    addCouponCode() {
      const vm = this
      const api = `${process.env.VUE_APP_APIPATH}/api/${process.env.VUE_APP_CUSTOMPATH}/coupon`
      const coupon = {
        code: vm.coupon_code
      }
      vm.isLoading = true
      this.$http.post(api, { data: coupon }).then(response => {
        // console.log('優惠卷', response)
        vm.getCart()
        vm.coupon_code = ''
        vm.isLoading = false
      })
    },
    goForm() {
      const vm = this
      vm.$router.push('/payment/form')
    }
  },
  created() {
    $(function() {
      $('[data-toggle="tooltip"]').tooltip()
    }),
      this.getCart()
  },
  components: {
    Navbar
  }
}
</script>

<style scoped></style>
