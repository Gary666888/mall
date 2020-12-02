<template>
  
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
  import BScroll, { PullUpLoad } from 'better-scroll'

  export default {
    name: "Scroll",
    props: {
      probeType: {
        type: Number,
        default: 0
      },
      PullUpLoad: {
        type: Boolean,
        default: false
      }
    },
    data() {
      return {
        scroll: null,
        message: 'hhhh'
      }
    },
    mounted() {
      this.scroll = new BScroll(this.$refs.wrapper,{
        click: true,
        probeType: this.probeType,
        PullUpLoad: this.PullUpLoad
      })
      this.scroll.on('scroll',(position) => {
        this.$emit('scroll',position)
      })
      this.scroll.on('scrollEnd', (pos)=>{
        this.$emit('scrollend', {endY: pos.y, maxY: this.scroll.maxScrollY})
        })
    },
    methods: {
      scrollTo(x,y,time = 300) {
        this.scroll.scrollTo(x,y,time)
      },
      refresh() {
        this.scroll.refresh()
      }
    }
  }

</script>
<style scoped>
</style>