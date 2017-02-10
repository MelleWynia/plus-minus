<template>
  <div class="hello">
    <h1>{{ count }}</h1>
    <button class="button-plus" v-on:mousedown="plus">PLUS</button>
    <button class="button-minus"
      v-on:mousedown="minus"
      v-on:mouseup="minusMouseup"
      v-on:touchend="minusMouseup"
    >MINUS</button>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      count: localStorage.count || 0,
      total: localStorage.total || 0,
      timer: false
    }
  },
  methods: {
    plus: function () {
      this.count++
      localStorage.count = this.count
      this.total++
      localStorage.total = this.total
    },
    minus: function () {
      this.count--
      localStorage.count = this.count

      this.timer = setTimeout(() => {
        this.count = 0
        localStorage.count = 0
      }, 1000)
    },
    minusMouseup: function () {
      clearTimeout(this.timer)
    },
    minusTouchup: function (event) {
      clearTimeout(this.timer)
      event.preventDefault()
    }
  },
  watch: {
    count: function (val) {
      document.title = val
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>

.hello
  margin 0 auto
  max-width 320px
  text-align center
  font-family Oswald, sans-serif

h1
  margin 10vh 0 16px 0
  padding 0
  font-size 84px

.button-plus
  display block
  padding 189px 9px 8px 0
  border 0
  background #9bd9fc
  font-size 26px
  width 100%
  text-align right
  letter-spacing 0.05rem
  font-weight 900
  transition 62ms

  &:active
    background lighten(#9bd9fc, 30%)
    transition none

  &:focus
    outline 0

.button-minus
  margin 26px
  padding 26px 7px 6px 100px
  border 0
  background lighten(#a69a47, 10%)
  font-weight bold
  font-size 14px
  transition 62ms
  color #000

  &:active
    background lighten(#a69a47, 30%)
    transition none

  &:focus
    outline 0


</style>
