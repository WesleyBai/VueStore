<template>
  <div>
    <!------------ 圖片抓下來放到檔案裡 -------------->
    <Navbar />
    <div
      id="carouselExampleIndicators"
      class="carousel slide carousel-fade"
      data-ride="carousel"
      data-interval="3000"
    >
      <ol class="carousel-indicators">
        <li
          data-target="#carouselExampleIndicators"
          data-slide-to="0"
          class="active bg-dark"
        ></li>
        <li
          data-target="#carouselExampleIndicators"
          data-slide-to="1"
          class="bg-dark"
        ></li>
        <li
          data-target="#carouselExampleIndicators"
          data-slide-to="2"
          class="bg-dark"
        ></li>
      </ol>
      <div class="carousel-inner">
        <div class="carousel-item active  carousel-bgc-1"></div>
        <div class="carousel-item  carousel-bgc-2"></div>
        <div class="carousel-item  carousel-bgc-3"></div>
      </div>
      <a
        class="carousel-control-prev"
        href="#carouselExampleIndicators"
        role="button"
        data-slide="prev"
      >
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="sr-only">Previous</span>
      </a>
      <a
        class="carousel-control-next"
        href="#carouselExampleIndicators"
        role="button"
        data-slide="next"
      >
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="sr-only">Next</span>
      </a>
    </div>

    <div class="container">
      <div class="row py-5">
        <div class="col-4">
          <div class="card border-0" style="background-color: #181A1B">
            <a href="#" class="card-body card-bgc-1"></a>
            <div class="card-footer text-center border-0 pb-0">
              <button class="btn btn-outline-dark border-secondary text-white">
                新品上市
              </button>
            </div>
          </div>
        </div>
        <div class="col-4">
          <div class="card border-0" style="background-color: #181A1B">
            <a href="#" class="card-body card-bgc-2"></a>
            <div class="card-footer text-center border-0 pb-0">
              <button class="btn btn-outline-dark border-secondary text-white">
                熱銷推薦
              </button>
            </div>
          </div>
        </div>
        <div class="col-4">
          <div class="card border-0" style="background-color: #181A1B">
            <a href="#" class="card-body card-bgc-3"></a>
            <div class="card-footer text-center border-0 pb-0">
              <button class="btn btn-outline-dark border-secondary text-white">
                特價商品
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div
      class="jumbotron jumbotron-fluid d-flex align-items-center mb-0 jumbotron-1"
    >
      <div class="container">
        <div class="d-flex justify-content-end">
          <button class="btn btn-dark">夏季優惠</button>
        </div>
      </div>
    </div>

    <div class="container-fluid px-2 py-5">
      <div class="form-row">
        <div class="col-md-8">
          <div class="form-row">
            <div class="col-md-5 mt-gutter">
              <div class="card card-radius-right card-photo-top">
                <div class="card-body"></div>
                <div class="card-footer text-center border-0">
                  <button class="btn btn-dark">Tops</button>
                </div>
              </div>
            </div>
            <div class="col-md-7 mt-gutter">
              <div class="card card-photo-coat">
                <div class="card-body"></div>
                <div class="card-footer text-center border-0">
                  <button class="btn btn-dark">Coat</button>
                </div>
              </div>
            </div>
            <div class="col-md-8 mt-gutter">
              <div class="card card-radius-rigth card-photo-suit">
                <div class="card-body"></div>
                <div
                  class="card-footer text-center border-0card-footer text-center border-0"
                >
                  <button class="btn btn-dark">Suit</button>
                </div>
              </div>
            </div>
            <div class="col-md-4 mt-gutter">
              <div class="card card-photo-shoes">
                <div class="card-body"></div>
                <div
                  class="card-footer text-center border-0card-footer text-center border-0"
                >
                  <button class="btn btn-dark">Shoes</button>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="col-md-4">
          <div class="form-row">
            <div class="col-12 mt-gutter">
              <div class="card card-radius-left card-photo-bottoms">
                <div class="card-body"></div>
                <div class="card-footer text-center border-0">
                  <button class="btn btn-dark">Bottoms</button>
                </div>
              </div>
            </div>
            <div class="col-md-12 mt-gutter">
              <div class="card card-radius-left card-photo-accessories">
                <div class="card-body"></div>
                <div class="card-footer text-center border-0">
                  <button class="btn btn-dark">Accessories</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div
      class="jumbotron jumbotron-fluid d-flex align-items-center mb-0 jumbotron-2"
    >
      <div class="container">
        <button class="btn btn-dark">優惠資訊</button>
      </div>
    </div>

    <div class="container py-5" id="tag">
      <div class="row">
        <div class="col-md-7">
          <iframe
            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2814.3265843174277!2d121.54883004515727!3d25.04214824382953!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3442abc50ad89187%3A0xd1bbed18c5665961!2z5b-g5a2d5pWm5YyW56uZ!5e0!3m2!1szh-TW!2stw!4v1561515120612!5m2!1szh-TW!2stw"
            width="100%"
            height="550"
            frameborder="0"
            style="border:0"
            allowfullscreen
          ></iframe>
        </div>
        <div
          class="col-md-5 d-flex align-items-center justify-content-center mt-2"
        >
          <div>
            <h2 class="mb-4">店舖位置</h2>
            <p>台北市大安區忠孝東路四段182號</p>
            <p>Mon - Fri, 8:30am - 10:30pm</p>
            <p>Saturday, 8:30am - 10:30pm</p>
            <p>Sunday, 8:30am - 10:30pm</p>
            <button class="btn btn-dark px-5 mt-2">取得位置</button>
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
    return {}
  },

  methods: {
    login() {
      const vm = this
      vm.$router.push(`/admin/products`)
    },
    signout() {
      const api = `${process.env.VUE_APP_APIPATH}/logout`
      const vm = this
      this.$http.post(api).then(response => {
        // console.log(response.data)
      })
    }
  },
  components: {
    Navbar
  }
}
</script>
