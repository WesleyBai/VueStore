<template>
  <div>
    <Navbar />
    <div class="container my-5">
      <div class="h1 text-center mb-5">紳士衣櫥</div>
      <div class="form-row text-center mb-5 text-white">
        <div class="col-md">
          <div class="alert alert-disable rounded-pill">1.確認商品內容</div>
        </div>
        <div class="col-md">
          <div class="alert alert-disable rounded-pill">2.填寫個人資料</div>
        </div>
        <div class="col-md">
          <div class="alert alert-active rounded-pill">3.完成訂單</div>
        </div>
      </div>
      <div class="row justify-content-center">
        <form class="col-md-8 border p-3" @submit.prevent="parOrder">
          <!--送出資料後觸發parOrder讓後端資料的order.is_paid更新-->
          <div class="h3 text-center py-3">訂單資訊</div>
          <table class="table text-white">
            <thead>
              <tr>
                <th width="150"></th>
                <th>品名</th>
                <th width="100">數量</th>
                <th width="100">單價</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item in order.products" :key="item.id">
                <!--將vm.order獲取的資料帶入-->
                <td>
                  <img :src="item.product.imageUrl" class="w-100 p-1 border" />
                </td>
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
              <tr>
                <td colspan="3" class="text-right">總計</td>
                <td class="text-right">{{ order.total | currency }}</td>
              </tr>
            </tfoot>
          </table>

          <table class="table text-white">
            <tbody>
              <tr>
                <th width="150">Email</th>
                <td>{{ order.user.email }}</td>
              </tr>
              <tr>
                <th>姓名</th>
                <td>{{ order.user.name }}</td>
              </tr>
              <tr>
                <th>收件人電話</th>
                <td>{{ order.user.tel }}</td>
              </tr>
              <tr>
                <th>收件人地址</th>
                <td>{{ order.user.address }}</td>
              </tr>
              <tr>
                <th>付款狀態</th>
                <td>
                  <span v-if="!order.is_paid" class="text-danger"
                    >尚未付款</span
                  >
                  <!--觸發parOrder更新資料後order.is_paid將變更為ture-->
                  <span v-else class="text-success">付款完成</span>
                  <!--最後畫面上將從尚未付款變更為顯示付款完成-->
                </td>
              </tr>
            </tbody>
          </table>
          <div class="text-right" v-if="order.is_paid === false">
            <!--尚未觸發parOrder更新order.is_paid時為false畫面會顯示 確認付款去 付款後就會消失-->
            <button class="btn btn-info">點此完成付款</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from '@/components/forestage/Navbar'

export default {
  data() {
    return {
      orderId: '',
      order: {
        user: {}
      }
    }
  },
  methods: {
    getOrder() {
      const vm = this
      const api = `${process.env.VUE_APP_APIPATH}/api/${process.env.VUE_APP_CUSTOMPATH}/order/${vm.orderId}` //從後端取的orderId
      vm.isLoading = true
      this.$http.get(api).then(response => {
        vm.order = response.data.order
        // console.log('結帳資料', response)
        vm.isLoading = false
      })
    },
    parOrder() {
      const vm = this
      const api = `${process.env.VUE_APP_APIPATH}/api/${process.env.VUE_APP_CUSTOMPATH}/pay/${vm.orderId}`
      vm.isLoading = true
      this.$http.post(api).then(response => {
        if (response.data.success) {
          this.$bus.$emit('message:push', '已成功付款', 'success')
          // console.log('付款完成', response)
        }
        this.getOrder() //重新取得訂單資料 以更新order.is_paid為ture後的畫面
        vm.isLoading = false
      })
    }
  },

  created() {
    this.orderId = this.$route.params.orderId //對應route中的orderId
    this.getOrder()
  },
  components: {
    Navbar
  }
}
</script>
