<template>
  <section class="header_box">
    <div class="header_inner">
      <span class="header_text">{{text_title}}</span>
      <span class="header_select" @click.prevent="selectEvent"></span>
      <app-scroll slot="headerSelect" :webData="innerList" ref="scroll" v-if="flag" @showChange="showChange"></app-scroll>
    </div>
  </section>
</template>

<script>
import appScroll from './scroll'
 export default {
   components: {
     appScroll
   },
   props: {
     headerTitle: String
   },
   methods: {
     selectEvent () {
       this.innerList = this.webList
       //this.$refs.scroll.$el.style.top = 420+'px'
       this.flag = !this.flag
     },
     showChange (item) {
       this.flag = ! this.flag
       this.text_title = item.name
       this.webIndex = item.num
     },
   },
   watch: {
       webIndex (cur, old) {
         this.$emit('webChange', cur)
       }
    },
   data () {
     return {
       text_title: '全部网点',
       webIndex: '111',
       flag: false,
       innerList: [
        'web1',
        'web2',
        'web3'
       ],
       webList: [
          {name: "网点1", num: '111'},
          {name: "网点2", num: '222'},
          {name: "网点3", num: '333'},
          {name: "网点4", num: '444'},
          {name: "网点5", num: '555'},
          {name: "网点6", num: '666'},
          {name: "网点7", num: '777'},
          {name: "网点8", num: '888'},
          {name: "网点9", num: '999'},
          {name: "网点10", num: '1010'}
       ]
     }
   }
 }

</script>

<style>
  .header_box {
    border-bottom: 1px solid #eee;
  }
  .header_inner {
    font-size:  30rpx;
    height :80rpx;
    display: flex; 
    justify-content: center;
    align-items: center;
  }
     .header_text {
       height: 100%;
       width: 3rem;
       display: flex;
       align-items: center;
       justify-content: center;
     }
     .header_select {
       height: 30rpx;
       width: 30rpx;
       border-radius: 15rpx;
       background: #ccc;
       position: absolute;
       right: 36%;
       margin-left: 10rpx;
     }
     .select_list {
        height: 5rem;
        width: 100%;
        border:1px solid #eee;
        bottom: 0;
     }
</style>