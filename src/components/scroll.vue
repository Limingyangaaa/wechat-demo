<template>
   <section class="scroll_box" ref="scrollMain">
     <div class="scroll_inner" v-for="(item, index) in webData">
      <div class="scroll_item" @click="detailEvent(item)">{{item.name}}</div>
     </div>
   </section>
</template>
<script>


export default {
  methods: {
    detailEvent (item) {
      this.$emit('showChange', item)
    }
  },
  props: {
    webData: {
      type: Array,
      default: []
    }
  },
  data () {
    return {
      showList: [],
      web1List: [
       {name: "网点1", num: '111'},
       {name: "网点2", num: '222'},
       {name: "网点3", num: '333'},
       {name: "网点4", num: '444'},
       {name: "网点5", num: '555'},
       {name: "网点6", num: '666'},
       {name: "网点7", num: '777'},
       {name: "网点8", num: '888'},
       {name: "网点9", num: '999'},
       {name: "网点10", num: '101010'}
      ]
    }
  }
}

</script>
<style>
.scroll_box{
  position: fixed;
  height: 6rem;
  width: 100%;
  border-top:1px solid #ccc;
  left:0;
  bottom:0;
  overflow-y: scroll;
  z-index: 10000000;
  background: #fff;
}

.scroll_inner{
  background: rgba(0, 0, 0, .1);
}

.scroll_item {
  font-size: 30rpx;
  height: 60rpx;
  margin-bottom: 6rpx;
  display: flex;
  justify-content:center;
  align-items: center;
}
</style>