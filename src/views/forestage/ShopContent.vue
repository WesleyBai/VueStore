<template>
  <div>
    <loading :active.sync="isLoading"></loading>
    <Cart
      class="position-fixed p-1"
      style="top: 12px; right: 15px; z-index:2000;"
      :navCart="cart"
      :navCartItem="cartitem"
      @cartCar="getCart"
    />
    <Navbar />
    <div class="container py-5">
      <div class="row d-flex justify-content-center mt-5">
        <div class="col-12 col-md-6 col-lg-5">
          <div
            class="imgSize mt-4 mt-md-0"
            :style="{ backgroundImage: `url(${product.imageUrl})` }"
          ></div>
        </div>
        <div class="col-12 col-md-6 col-lg-5">
          <h2 class="mt-4 mt-md-0 text-center text-md-left">
            <strong>{{ product.title }}</strong>
          </h2>
          <div class="text-center text-md-left">
            <span class="h3 text-info" v-if="product.price"
              ><strong>{{ product.price | currency }}元</strong>
            </span>
            <span v-if="product.origin_price > 0">
              <del class="h5 text-secondary ml-5"
                >原價 {{ product.origin_price | currency }}元
              </del>
            </span>
            <span class="h3 text-info" v-if="!product.price"
              ><strong>{{ product.origin_price | currency }}元</strong></span
            >
          </div>

          <div class="mt-4">
            <label for="num" class="h6">數量</label>
            <select id="num" v-model="product.num" class="form-control">
              <option :value="num" v-for="num in 10" :key="num.id">
                選購 {{ num }} {{ product.unit }}
              </option>
            </select>
          </div>
          <button
            class="btn btn-info mt-3 w-100"
            @click="addtoCart(product.id, product.num)"
          >
            <i
              class="fas fa-spinner fa-spin"
              v-if="status.loadingItem === product.id"
            ></i
            >加入購物車
          </button>
          <div class="mt-4 text-center text-md-left ">
            <div class="d-md-none">
              <h2 class="mt-4 mt-md-0 text-center text-md-left">
                <strong>{{ product.title }}</strong>
              </h2>
            </div>
            <h5 class="text-info"><strong>商品介紹</strong></h5>
            <p>{{ product.description }}</p>
            <p>{{ product.content }}</p>
            <p>製造：台灣</p>
            <hr />
          </div>
          <div class="text-center text-md-left ">
            <h5 class="text-info"><strong>開幕優惠</strong></h5>
            <i class="fas fa-thumbs-up mr-2"></i>結帳時可輸入優惠碼享折扣
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Cart from '@/components/forestage/Cart'
import Navbar from '@/components/forestage/Navbar'
export default {
  data() {
    return {
      product: {},
      itemId: '',
      isLoading: false,
      status: {
        loadingItem: ''
      },
      cart: [],
      cartitem: []
    }
  },
  methods: {
    getProduct(id) {
      const vm = this
      const api = `${process.env.VUE_APP_APIPATH}/api/${process.env.VUE_APP_CUSTOMPATH}/product/${id}`
      vm.isLoading = true
      this.$http.get(api).then(response => {
        vm.product = response.data.product
        // console.log('商品資訊', response.data.product)
        vm.isLoading = false
      })
    },

    addtoCart(id, qty = 1) {
      const vm = this
      const api = `${process.env.VUE_APP_APIPATH}/api/${process.env.VUE_APP_CUSTOMPATH}/cart`
      vm.status.loadingItem = id
      const cart = {
        product_id: id,
        qty
      }
      this.$http.post(api, { data: cart }).then(response => {
        vm.getCart()
        vm.status.loadingItem = ''
        this.$bus.$emit('message:push', '商品已加入購物車', 'yellow')
      })
    },

    getCart() {
      const vm = this
      const api = `${process.env.VUE_APP_APIPATH}/api/${process.env.VUE_APP_CUSTOMPATH}/cart`
      this.$http.get(api).then(response => {
        vm.cart = response.data.data
        vm.cartitem = response.data.data.carts.length
        // console.log('購物車資料', response.data)
      })
    }
  },
  created() {
    this.itemId = this.$route.params.itemId //須和路由設置一樣id名稱
    this.getProduct(this.itemId)
    this.getCart()
  },
  components: {
    Cart,
    Navbar
  }
}
</script>

<style lang="scss" scoped></style>
