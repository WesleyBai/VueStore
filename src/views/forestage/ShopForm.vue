<template>
  <div>
    <loading :active.sync="isLoading"></loading>
    <Navbar />
    <div class="container py-5">
      <div class="h1 text-center mb-5">紳士衣櫥</div>
      <div class="form-row text-center mb-5 text-white">
        <div class="col-md">
          <div class="alert alert-disable rounded-pill">1.確認商品內容</div>
        </div>
        <div class="col-md">
          <div class="alert alert-active rounded-pill">2.填寫個人資料</div>
        </div>
        <div class="col-md">
          <div class="alert alert-disable rounded-pill">3.完成訂單</div>
        </div>
      </div>

      <div class="row justify-content-center">
        <div class="col-md-8 border p-3">
          <form @submit.prevent="creatOrder">
            <div class="h3 text-center py-3">訂購人資訊</div>
            <div class="form-row">
              <div class="form-group col-md-6">
                <label for="username">收件人姓名</label>
                <input
                  type="text"
                  class="form-control input-color"
                  name="name"
                  id="username"
                  v-model="form.user.name"
                  v-validate="'required'"
                  :class="{ 'is-invalid': errors.has('name') }"
                  placeholder="請輸入姓名"
                />
                <span class="text-danger" v-if="errors.has('name')">
                  <i class="fas fa-exclamation-circle"></i> 姓名欄位 不得留空。
                </span>
              </div>

              <div class="form-group col-md-6">
                <label for="usertel">收件人電話</label>
                <input
                  type="tel"
                  class="form-control input-color"
                  name="tel"
                  id="usertel"
                  v-model="form.user.tel"
                  v-validate="'required'"
                  :class="{ 'is-invalid': errors.has('tel') }"
                  placeholder="請輸入電話"
                />
                <span class="text-danger" v-if="errors.has('tel')">
                  <i class="fas fa-exclamation-circle"></i> 電話欄位 不得留空。
                </span>
              </div>
              <div class="form-group col-md-12">
                <label for="useremail">Email</label>
                <input
                  type="email"
                  class="form-control input-color"
                  name="email"
                  id="useremail"
                  v-model="form.user.email"
                  v-validate="'required|email'"
                  :class="{ 'is-invalid': errors.has('email') }"
                  placeholder="請輸入 Email"
                />
                <span class="text-danger" v-if="errors.has('email')">
                  <i class="fas fa-exclamation-circle"></i>
                  {{ errors.first('email') }}
                </span>
              </div>

              <!-- <div class="form-group col-md">
                <label for="country">國家</label>
                <select id="country" class="form-control" required>
                  <option selected>1</option>
                  <option>2</option>
                  <option>3</option>
                </select>
              </div>
              <div class="form-group col-md">
                <label for="city">城市</label>
                <select id="city" class="form-control" required>
                  <option selected>Choose...</option>
                  <option>...</option>
                  <option>...</option>
                </select>
              </div>-->

              <!-- <div class="form-group col-md">
                <label for="userzip">郵遞區號</label>
                <input
                  type="text"
                  class="form-control"
                  name="zip"
                  id="userzip"
                  v-model="form.user.zip"
                  v-validate="'required'"
                  :class="{'is-invalid': errors.has('zip')}"
                  placeholder="請輸入郵遞區號"
                />
                <span class="text-danger" v-if="errors.has('zip')">
                  <i class="fas fa-exclamation-circle"></i> 郵遞區號 不得留空。
                </span>
              </div>-->

              <div class="form-group col-md-12">
                <label for="useraddress">收件人地址</label>
                <input
                  type="text"
                  class="form-control input-color"
                  name="address"
                  id="useraddress"
                  v-model="form.user.address"
                  v-validate="'required'"
                  :class="{ 'is-invalid': errors.has('address') }"
                  placeholder="請輸入地址"
                />
                <span class="text-danger" v-if="errors.has('address')">
                  <i class="fas fa-exclamation-circle"></i> 地址欄位 不得留空。
                </span>
              </div>
            </div>

            <div class="text-right">
              <button class="btn btn-success">送出訂單</button>
            </div>
          </form>
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
      isLoading: false,
      form: {
        user: {
          name: '',
          email: '',
          tel: '',
          zup: '',
          address: ''
        },
        message: ''
      }
    }
  },
  methods: {
    creatOrder() {
      const vm = this
      const api = `${process.env.VUE_APP_APIPATH}/api/${process.env.VUE_APP_CUSTOMPATH}/order`
      vm.isLoading = true
      const order = vm.form
      this.$validator.validate().then(result => {
        if (result) {
          this.$http.post(api, { data: order }).then(response => {
            // console.log('建立訂單', response.data)
            if (response.data.success) {
              vm.$router.push(`/payment/check/${response.data.orderId}`) //確保傳入orderId
            }
            vm.isLoading = false
          })
        } else {
          // console.log('欄位輸入不完整')
          this.$bus.$emit('message:push', '欄位輸入不完整', 'danger')
          vm.isLoading = false
        }
      })
    }
  },
  components: {
    Navbar
  }
}
</script>
