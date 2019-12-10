<template>
  <div id="app">
    <vheader :seller="seller"></vheader>
    <div class="tab-wrapper">
      <tab :tabs="tabs" :initialIndex=0></tab>
    </div>
  </div>
</template>

<style lang="less" scoped>
.tab-wrapper{
  position: fixed;
  top: 136px;
  left: 0;
  right: 0;
  bottom: 0;
  
}
</style>
<script>
import vheader from 'components/header/vheader.vue'
import {getSeller} from 'api'
import Goods from 'components/goods/goods'
import Ratings from 'components/ratings/ratings'
import Seller from 'components/seller/seller'
import tab from 'components/tab/tab'

export default {
  data(){
    return{
      seller:""
    }
  },
  computed:{
    tabs(){
      return [
        {
          label:'商品',
          components:Goods,
          data:{
            seller:this.seller
          }
        },
        {
          label:'评论',
          components:Ratings,
          data:{
            seller:this.seller
          }
        },
        {
          label:'商家',
          components:Seller,
          data:{
            seller:this.seller
          }
        },
      ]
    }
  },
  components:{
    vheader,
    tab
  },
  created(){
    this._getSeller()
  },
  methods:{
    _getSeller(){
      getSeller({}).then((seller)=>{
        this.seller=seller;
      })
    }
  }
}
</script>
