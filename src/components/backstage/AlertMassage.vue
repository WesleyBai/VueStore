<template>
  <div class="message-alert">
    <div
      class="alert alert-dismissible animated jackInTheBox
"
      :class="'alert-' + item.status"
      v-for="(item, i) in messages"
      :key="i"
    >
      {{ item.message }}
      <button
        type="button"
        class="close"
        @click="removeMessage(i)"
        aria-label="Close"
      >
        <span aria-hidden="true">&times;</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'alert',
  data() {
    return {
      messages: []
    }
  },
  methods: {
    updateMessage(message, status) {
      const timestamp = Math.floor(new Date() / 1000)
      this.messages.push({
        message, //訊息的內容
        status, //訊息顯示的樣式
        timestamp //訊息多久會消失
      })
      this.removeMessageWithTiming(timestamp) //觸發清除訊息的函式(removeMessageWithTiming)
    },
    removeMessage(num) {
      this.messages.splice(num, 1) //訊息右上角的主動清除按鈕
    },
    removeMessageWithTiming(timestamp) {
      // 執行函式後 5秒後清除訊息
      const vm = this
      setTimeout(() => {
        vm.messages.forEach((item, i) => {
          if (item.timestamp === timestamp) {
            vm.messages.splice(i, 1)
          }
        })
      }, 4000)
    }
  },
  created() {
    const vm = this

    // 自定義名稱 'messsage:push'
    // message: 傳入參數
    // status: 樣式，預設值為 warning
    vm.$bus.$on('message:push', (message, status = 'warning') => {
      //使用on 註冊 'message:push'的方法, (訊息內容, Alert樣式)
      vm.updateMessage(message, status)
    })
    // vm.$bus.$emit('message:push');    //觸發外層使用$on  觸發內層使用$emit
  }
}
</script>
