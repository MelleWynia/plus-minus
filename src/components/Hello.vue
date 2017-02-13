<template>
  <div class="hello">
    <h1
      v-bind:class="{ '___is-minus': count < 0 }"
    >
      {{ count }}
    </h1>
    <button
      class="button-plus"
      v-on:mousedown="plus"
      v-on:touchstart="plus"
    >PLUS</button>
    <button class="button-minus"
      v-on:mousedown="minus"
      v-on:touchstart="minus"
      v-on:mouseup="minusMouseup"
      v-on:touchend="minusMouseup"
    >MINUS</button>
  </div>
</template>

<script>

document.title = localStorage.count || 0

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
    plus: function (event) {
      this.count++
      localStorage.count = this.count
      this.total++
      localStorage.total = this.total

      event.preventDefault()
    },
    minus: function (event) {
      event.preventDefault()
      this.count--
      localStorage.count = this.count

      this.timer = setTimeout(() => {
        this.count = 0
        localStorage.count = 0
      }, 1000)
    },
    minusMouseup: function (event) {
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

.not-selectable
  -webkit-touch-callout none
  -webkit-user-select none
  -khtml-user-select none
  -moz-user-select none
  -ms-user-select none
  user-select none
  -webkit-tap-highlight-color rgba(0,0,0,0)

.hello
  margin 0 auto
  max-width 320px
  text-align center
  font-family Oswald, sans-serif

h1
  margin 0
  padding 4vh 0 0 0
  font-size 84px
  text-shadow 0 0 10px rgba(#9bd9fc, 0.26)
  transition color 380ms

  @media (min-height: 530px)
    padding-top 11vh

  &.___is-minus
    color #c59a1e
    text-shadow 0 0 10px rgba(#c59a1e, 0.26)
    text-indent: -29px;

.button-plus
  display block
  padding 189px 9px 8px 0
  border 0
  box-shadow 0 0 26px rgba(#9bd9fc, 0.38)
  background #8bd5ff
  font-size 26px
  width 100%
  text-align right
  letter-spacing 0.05rem
  font-weight 900
  transition 380ms
  text-shadow 0 0 10px rgba(#000, 0.1)

  @extends .not-selectable

  &:active
    background lighten(#8bd5ff, 50%)
    transition none

  &:focus
    outline 0

.button-minus
  margin 16px
  padding 26px 7px 6px 100px
  border 0
  box-shadow 0 0 10px rgba(#c59a1e, 0.62)
  background #c59a1e
  font-weight 900
  font-size 14px
  transition 380ms
  color #000
  text-shadow 0 0 10px rgba(#000, 0.1)

  @extends .not-selectable

  &:active
    background lighten(#c59a1e, 40%)
    transition none

  &:focus
    outline 0


</style>
