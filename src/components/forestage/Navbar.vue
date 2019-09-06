<template>
  <div>
    <nav
      class="navbar navbar-expand-md navbar-dark py-2 dropdown fixed-top"
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
      <div class="navbar-collapse collapse" id="navbarNavDropdown">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active mr-5">
            <a href="#" class="nav-link back" @click="home">
              回首頁
              <span class="sr-only">(current)</span>
            </a>
          </li>
          <li class="nav-item active mr-5" style="padding-right:14.4px">
            <router-link class="nav-link" to="/shop">
              商品
              <span class="sr-only">(current)</span>
            </router-link>
          </li>

          <li class="nav-item active mr-5">
            <a class="nav-link" href="#">
              關於衣櫥
              <span class="sr-only">(current)</span>
            </a>
          </li>
          <li class="nav-item active">
            <a class="nav-link" href="#" @click="map">
              衣櫥位置
              <span class="sr-only">(current)</span>
            </a>
          </li>
        </ul>

        <form class="form-inline mtop mr-5">
          <a
            href="#"
            class="btn btn-outline-info mr-2"
            style="width:46px;"
            data-toggle="modal"
            data-target="#loginModal"
          >
            <i class="fas fa-user"></i>
          </a>

          <a href="#" class="btn btn-outline-info" @click.prevent="login">
            <i class="fas fa-user-cog"></i>
          </a>
        </form>
      </div>
    </nav>

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
        <div class="modal-content bg-dark border-0">
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
                  class="form-control input-color"
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
                  class="form-control input-color"
                  id="registerPassWord"
                  placeholder="Password"
                  required
                />
              </div>
              <div class="form-group">
                <div class="form-check">
                  <input
                    class="form-check-input input-color"
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
              class="mr-auto text-decoration-none"
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
        <div class="modal-content bg-dark  border-0">
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
                      class="form-control input-color"
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
                      class="form-control input-color"
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
                      class="form-control input-color"
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
              class="mr-auto text-decoration-none"
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

export default {
  data() {
    return {
      categories: ''
    }
  },
  methods: {
    login() {
      const vm = this
      const api = `${process.env.VUE_APP_APIPATH}/api/${process.env.VUE_APP_CUSTOMPATH}/admin/products`
      this.$http.get(api).then(response => {
        if (response.data.success) {
          vm.$router.push(`/admin/products`)
          console.log(response.data)
        } else {
          const api = `${process.env.VUE_APP_APIPATH}/logout` //api路徑
          this.$http.post(api).then(response => {
            vm.$router.push('/login') //如果成功的話 將頁面轉移到home
            console.log(response.data)
          })
        }
      })
    },
    home() {
      const vm = this
      vm.$router.push('/')
    },
    join() {
      const vm = this
      vm.$router.push('/join')
    },
    map() {
      const vm = this
      $('html, body').animate({ scrollTop: 3390 }, 500)
      vm.$router.push('/')
    }
  }
}
</script>
