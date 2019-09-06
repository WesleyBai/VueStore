<template>
  <div>
    <button
      type="button"
      class="btn btn-info gotop animated slow"
      @click.prevent="backtop"
    >
      <i class="fas fa-arrow-up"></i>
    </button>
  </div>
</template>

<script>
import $ from 'jquery'

export default {
  data() {
    return {}
  },
  methods: {
    backtop() {
      $('html, body').animate({ scrollTop: 0 }, 600)
    }
  },
  created() {
    $(function() {
      $(window).scroll(function() {
        if ($(this).scrollTop() >= $(window).height()) {
          $('.gotop')
            .addClass('scrolltop')
            .addClass('bounce')
        } else {
          $('.gotop').removeClass('scrolltop')
        }
      })
    })
  }
}
</script>
