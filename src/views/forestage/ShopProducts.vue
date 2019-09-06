<template>
  <div>
    <loading :active.sync="isLoading"></loading>
    <Cart
      class="animated tada position-fixed p-1"
      style="top: 12px; right: 15px; z-index:2000;"
      :navCart="cart"
      :navCartItem="cartitem"
      @cartCar="getCart"
    />
    <nav
      class="navbar navbar-expand-md 
      navbar-dark py-2 dropdown 
      fixed-top border-bottom"
      style="background-color: #1D1E20"
    >
      <div class="mr-5">
        <a
          href="#"
          class="navbar-brand text-decoration-none bg-transparent shadow-none"
          @click="home"
        >
          <i class="fas fa-store-alt text-info mr-2"></i>
          紳士衣櫥
        </a>

        <a href="#navbarNavDropdown" class="d-sm-none" data-toggle="collapse">
          <i class="fas fa-angle-down"></i>
        </a>
      </div>
      <div class="navbar-collapse" id="navbarNavDropdown">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active mr-5">
            <a href="#" class="nav-link" @click="home">
              回首頁
              <span class="sr-only">(current)</span>
            </a>
          </li>

          <!-- dropdown -->
          <li class="nav-item  active d-none d-sm-block mr-5 fadein">
            <a class="nav-link" href="#">
              商品
              <i class="fas fa-angle-down animated fadeInLeft"></i>
            </a>
            <div
              class="dropdown-menu w-100 py-3 rounded-0 bg-dark d-block fadeout"
            >
              <div class="container">
                <div class="row d-flex justify-content-around ">
                  <ul class="nav flex-column ">
                    <li class="nav-item ">
                      <a
                        class="nav-link h5 text-white active"
                        href="#"
                        :class="{ 'text-info': categories == '' }"
                        @click="categories = ''"
                      >
                        <strong>ALL</strong>
                      </a>
                    </li>
                  </ul>
                  <ul class="nav flex-column">
                    <li class="nav-item">
                      <a
                        class="nav-link h5 text-white active"
                        href="#"
                        :class="{ 'text-info': categories == '上衣' }"
                        @click="categories = '上衣'"
                      >
                        <strong>上衣</strong>
                      </a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">短 TEE</a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">襯衫</a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">外套</a>
                    </li>
                  </ul>
                  <ul class="nav flex-column">
                    <li class="nav-item">
                      <a
                        class="nav-link h5 text-white"
                        href="#"
                        :class="{ 'text-info': categories == '褲子' }"
                        @click="categories = '褲子'"
                      >
                        <strong>褲子</strong>
                      </a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">短褲</a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">長褲</a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">牛仔褲</a>
                    </li>
                  </ul>
                  <ul class="nav flex-column">
                    <li class="nav-item">
                      <a
                        class="nav-link h5 text-white"
                        href="#"
                        :class="{ 'text-info': categories == '配件' }"
                        @click="categories = '配件'"
                      >
                        <strong>配件</strong>
                      </a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">帽子</a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">包包</a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">鞋類</a>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </li>

          <!-- collapse -->
          <li class="nav-item active d-sm-none">
            <a
              class="nav-link"
              href="#navbarCollapseMenuLink"
              data-toggle="collapse"
            >
              商品
              <i class="fas fa-angle-down"></i>
            </a>
            <div class="collapse py-3 bg-dark" id="navbarCollapseMenuLink">
              <div class="container">
                <div class="row d-flex justify-content-around">
                  <ul class="nav flex-column">
                    <li class="nav-item">
                      <a
                        class="nav-link h5 text-white"
                        href="#"
                        :class="{ 'text-info': categories == '' }"
                        @click="categories = ''"
                      >
                        <strong>ALL</strong>
                      </a>
                    </li>
                  </ul>
                  <ul class="nav flex-column">
                    <li class="nav-item">
                      <a
                        class="nav-link h5 text-white"
                        href="#"
                        :class="{ 'text-info': categories == '上衣' }"
                        @click="categories = '上衣'"
                      >
                        <strong>上衣</strong>
                      </a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">短 TEE</a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">襯衫</a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">外套</a>
                    </li>
                  </ul>
                  <ul class="nav flex-column">
                    <li class="nav-item">
                      <a
                        class="nav-link h5 text-white"
                        href="#"
                        :class="{ 'text-info': categories == '褲子' }"
                        @click="categories = '褲子'"
                      >
                        <strong>褲子</strong>
                      </a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">短褲</a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">長褲</a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">牛仔褲</a>
                    </li>
                  </ul>
                  <ul class="nav flex-column">
                    <li class="nav-item">
                      <a
                        class="nav-link h5 text-white"
                        href="#"
                        :class="{ 'text-info': categories == '配件' }"
                        @click="categories = '配件'"
                      >
                        <strong>配件</strong>
                      </a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">帽子</a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">包包</a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link disabled" href="#">鞋類</a>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </li>

          <li class="nav-item active mr-5">
            <a class="nav-link" href="#">
              關於衣櫥
              <span class="sr-only">(current)</span>
            </a>
          </li>
          <li class="nav-item active">
            <a class="nav-link" href="#tag" @click="map">
              衣櫥位置
              <span class="sr-only">(current)</span>
            </a>
          </li>
        </ul>

        <form class="form-inline mtop pr-5">
          <a
            href="#"
            class="btn btn-outline-info mr-2"
            data-toggle="modal"
            data-target="#loginModal"
            style="width:46px;"
          >
            <i class="fas fa-user"></i>
          </a>

          <a href="#" class="btn btn-outline-info" @click.prevent="login">
            <i class="fas fa-user-cog"></i>
          </a>
        </form>
      </div>
    </nav>

    <div class="container pt-2">
      <div class="row">
        <div class="col-md">
          <div class="row">
            <div
              class="col-md-3 mb-4"
              v-for="item in filterData"
              :key="item.id"
              v-if="item.is_enabled"
            >
              <!--透過products將資料從後端取出再透過filterData篩選最後顯示在畫面上  v-if代表未啟用商品時不顯示-->
              <div class="card border-0">
                <a href="#" @click="getContent(item.id)">
                  <div
                    style="height: 400px; background-size: cover; background-position: center;"
                    :style="{ backgroundImage: `url(${item.imageUrl})` }"
                  ></div>
                </a>
                <div class="card-body bg-dark">
                  <div class="d-flex justify-content-between  m-0">
                    <h5>
                      <a
                        href="#"
                        @click="getContent(item.id)"
                        class="text-white text-decoration-none"
                        >{{ item.title }}
                      </a>
                    </h5>

                    <del class="h6 text-muted" v-if="item.origin_price > 0">
                      原價 {{ item.origin_price | currency }} 元
                    </del>
                  </div>

                  <div class="text-right">
                    <div class="h6" v-if="!item.price">
                      <span class="h5">{{ item.origin_price | currency }}</span>
                      元
                    </div>
                    <div class="h6" v-if="item.price">
                      <span class="h5">{{ item.price | currency }}</span>
                      元
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!--分頁props-->
      <!-- <Pagination :paginations="pagination" @getPage="getProducts" /> -->
    </div>

    <!--商品內容 模板-->
    <!-- <div
      class="modal fade"
      style="z-index:3000"
      id="productModal"
      tabindex="-1"
      role="dialog"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true">
      <div class="modal-dialog modal-lg" role="document">
        <div class="modal-content border-0 bg-dark">
          <div
            class="modal-header d-flex justify-content-center position-relative align-items-center"
          >
            <figure class="figure mb-0 p-2">
              <img
                :src="product.imageUrl"
                class="figure-img img-fluid rounded mb-0"
                alt="..."
              />
            </figure>
            <button
              type="button"
              class="close position-absolute "
              style="top: 0px; right: 4px;"
              data-dismiss="modal"
              aria-label="Close"
            >
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <blockquote class="blockquote">
              <p class="mb-0">{{ product.title }}</p>
              <footer class="blockquote-footer text-white text-right">
                {{ product.description }}
              </footer>
            </blockquote>

            <div class="row mt-5">
              <div class="col-md-8">
                <div class="pt-4">
                  <span class="h6">{{ product.content }}</span>
                </div>
              </div>
              <div class="col-md-4 text-right">
                <div v-if="!product.price">
                  <span class="h4 ">{{ product.origin_price | currency }}</span
                  >元
                </div>
                <del class="h5 text-muted" v-if="product.price">
                  原價
                  <span class="h5">{{ product.origin_price | currency }}</span
                  >元
                </del>

                <div class="h4" v-if="product.price">
                  現在只要
                  <span class="h4">{{ product.price | currency }}</span
                  >元
                </div>
              </div>
            </div>

            <select
              name
              class="form-control mt-3 input-color"
              v-model="product.num"
            >
              <option :value="num" v-for="num in 10" :key="num"
                >選購 {{ num }} {{ product.unit }}</option
              >
            </select>
          </div>
          <div class="modal-footer">
            <div class="text-nowrap mr-3">
              小計
              <strong>{{ (product.num * product.price) | currency }}</strong> 元
            </div>
            <button
              type="button"
              class="btn btn-primary"
              @click="addtoCart(product.id, product.num)"
            >
              <i
                class="fas fa-spinner fa-spin"
                v-if="product.id === status.loadingItem"
              ></i>
              加到購物車
            </button>
          </div>
        </div>
      </div>
    </div> -->

    <!-- 登入Modal -->

    <div
      class="modal fade"
      id="loginModal"
      tabindex="-1"
      role="dialog"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered" role="document">
        <div class="modal-content bg-dark">
          <div class="modal-header bg-yellow border-0">
            <h5 class="modal-title" id="exampleModalLabel">會員登入</h5>
            <button
              type="button"
              class="close"
              data-dismiss="modal"
              aria-label="Close"
            >
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <form>
              <div class="form-group">
                <label for="registerID">
                  信箱
                </label>
                <input
                  type="email"
                  class="form-control"
                  id="registerID"
                  aria-describedby="emailHelp"
                  placeholder="Email"
                  required
                />
              </div>
              <div class="form-group">
                <label for="registerPassWord">
                  密碼
                </label>
                <input
                  type="password"
                  class="form-control"
                  id="registerPassWord"
                  placeholder="Password"
                  required
                />
              </div>
              <div class="form-group">
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    id="remberMe"
                    required
                  />
                  <label class="form-check-label" for="remberMe">
                    記住帳號
                  </label>
                </div>
              </div>
            </form>
          </div>
          <div class="modal-footer">
            還沒有帳號？
            <a
              href="#"
              data-dismiss="modal"
              class="mr-auto"
              data-toggle="modal"
              data-target="#registerModal"
              >註冊會員</a
            >
            <button type="submit" class="btn btn-primary">登入</button>
          </div>
        </div>
      </div>
    </div>

    <!-- 註冊Modal -->
    <div
      class="modal fade "
      id="registerModal"
      tabindex="-1"
      role="dialog"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-lg modal-dialog-centered" role="document">
        <div class="modal-content bg-dark">
          <div class="modal-header bg-yellow border-0">
            <h5 class="modal-title" id="exampleModalLabel">
              註冊會員
            </h5>
            <button
              type="button"
              class="close"
              data-dismiss="modal"
              aria-label="Close"
            >
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="row">
              <div class="col-md-6">
                <h2>註冊紳士衣櫥</h2>
                <p>
                  Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt
                  error neque sint dicta inventore quas consequuntur ducimus.
                  Distinctio asperiores nisi a suscipit. Repellendus sequi
                  expedita fuga assumenda dolorem voluptatibus quia.
                </p>
                <p>
                  Lorem, ipsum dolor sit amet consectetur adipisicing elit.
                  Alias iure libero reiciendis sint beatae ratione quaerat?
                  Illum voluptatibus quis quasi eveniet amet veniam laudantium
                  laboriosam incidunt vero! Similique, libero delectus.
                </p>
              </div>
              <div class="col-md-6">
                <form>
                  <div class="form-group">
                    <label for="registerId">
                      信箱
                    </label>
                    <input
                      type="email"
                      class="form-control"
                      id="registerId"
                      aria-describedby="emailHelp"
                      placeholder="name@example.com"
                      required
                    />
                  </div>
                  <div class="form-group">
                    <label for="registerPassword">
                      密碼
                    </label>
                    <input
                      type="password"
                      class="form-control"
                      id="registerPassword"
                      placeholder="請輸入密碼"
                      required
                    />
                  </div>
                  <div class="form-group">
                    <label for="doubleCheck">
                      確認密碼
                    </label>
                    <input
                      type="password"
                      class="form-control"
                      id="doubleCheck"
                      placeholder="再次輸入密碼"
                      required
                    />
                  </div>
                  <div class="form-group">
                    <div class="form-check">
                      <input
                        class="form-check-input"
                        type="checkbox"
                        id="exampleCheck"
                        required
                      />
                      <label class="form-check-label" for="exampleCheck">
                        同意條款
                      </label>
                    </div>
                  </div>
                </form>
              </div>
            </div>
          </div>
          <div class="modal-footer">
            已經有帳號了？
            <a
              href="#"
              data-dismiss="modal"
              class="mr-auto"
              data-toggle="modal"
              data-target="#loginModal"
              >按此登入</a
            >

            <button type="submit" class="btn btn-primary">註冊</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import $ from 'jquery'
import Cart from '@/components/forestage/Cart'

export default {
  data() {
    return {
      products: [],
      product: {},
      cart: [],
      cartitem: [],
      pagination: {},
      status: {
        loadingItem: ''
      },
      isLoading: false,
      categories: '',
      fadeIn: ''
    }
  },
  methods: {
    getProducts(page) {
      const vm = this
      const api = `${process.env.VUE_APP_APIPATH}/api/${process.env.VUE_APP_CUSTOMPATH}/products?page=${page}`
      vm.isLoading = true
      this.$http.get(api).then(response => {
        vm.products = response.data.products
        vm.isLoading = false
        vm.pagination = response.data.pagination
        $('.drop-hover').mouseover(function() {
          $('.drop-hover').dropdown('show')
        })
        $('.drop-hover').mouseleave(function() {
          $('.drop-hover').dropdown('hide')
        })
        // console.log('販賣的物品', response.data.products)
      })
    },
    getContent(id) {
      const vm = this
      vm.$router.push(`content/${id}`)
    },

    getCart() {
      const vm = this
      const api = `${process.env.VUE_APP_APIPATH}/api/${process.env.VUE_APP_CUSTOMPATH}/cart`
      this.$http.get(api).then(response => {
        vm.cart = response.data.data
        vm.cartitem = response.data.data.carts.length
        // console.log('購物車資料', response.data)
      })
    },
    login() {
      const vm = this
      const api = `${process.env.VUE_APP_APIPATH}/api/${process.env.VUE_APP_CUSTOMPATH}/admin/products`
      this.$http.get(api).then(response => {
        if (response.data.success) {
          vm.$router.push(`/admin/products`)
          // console.log(response.data)
        } else {
          const api = `${process.env.VUE_APP_APIPATH}/logout` //api路徑
          this.$http.post(api).then(response => {
            vm.$router.push('/login') //如果成功的話 將頁面轉移到home
            // console.log(response.data)
          })
        }
      })
    },
    home() {
      const vm = this
      vm.$router.push('/')
    },
    map() {
      const vm = this
      $('html, body').animate({ scrollTop: 3390 }, 500)
      vm.$router.push('/')
    }
  },
  computed: {
    filterData() {
      //當選擇類別時會變更categories並執行此函式
      const vm = this
      if (vm.categories == '') {
        return vm.products
        //回傳全部商品
      } else {
        vm.filteritem = []
        vm.products.forEach(function(item) {
          if (vm.categories === item.category) vm.filteritem.push(item)
        })
        return vm.filteritem
        //回傳特定的商品
      }
    }
  },
  created() {
    this.getProducts()
    this.getCart()
  },
  components: {
    Cart
  }
}
</script>