<template>
  <div class="rrf-swiper" style="height:300px;">
      <div class="big-con">
        <div class="swiper-img" v-for="(item, index) in imgArr" :key="index">
                <a :href="item.url">
                <div class="picDiv" :data-index="index" v-swipeleft="(e)=>leftHandler(e)" v-swiperight="(e)=>rightHandler(e)" :style="{ backgroundImage:'url('+item.img+')'}"></div>
                </a>
        </div>
      </div>
      <div class="number">
          <strong>{{ currIndex }}</strong>
          <span>/</span>
          <i> {{ imgArr.length }} </i>
      </div>
  </div>
</template>

<script>
  import Vue from 'vue'
  import vueTouch from 'kim-vue-touch'
  Vue.use(vueTouch)

export default {
    name: 'RrfSwiper',
    components:{},
    props:{
        imgArr: {
            type: Array,
            required: false
        },
    },
    data(){
        return {
            currIndex: 1,
            swiperImgs: null,
            winWidth:0,
        }
    },
    watch:{},
    computed:{},
    methods:{
        leftHandler(e){
            var index = $(e.target).parents('.swiper-img').index()+1;
            if(index == this.imgArr.length) {
                this.$emit('fatherSwiper');
                return;
            }
            $('.big-con').css({transform:`translate3d(${-this.winWidth*index}px, 0, 0)`});
            this.currIndex++;
            this.effect();
        },
        rightHandler(e){
            var left = $('.big-con').offset().left;
            if(left == 0) return;
            $('.big-con').css({transform:`translate3d(${this.winWidth+left}px, 0, 0)`});
            this.currIndex--;
            this.effect();
        },
        effect(){
            $('.big-con').css('transition','all 300ms ease 0s');
        }
    },
    created(){},
    mounted(){
        this.winWidth = $('.rrf-swiper').width();
        $('.swiper-img').css('width',this.winWidth);
        $('.big-con').css('width',$('.swiper-img').width()*this.imgArr.length);
    }
}
</script>
<style lang="less" scoped>
.rrf-swiper {
    position: relative;
    .big-con{
        height:100%;
        position: absolute;
        z-index: 2;
    }
    .big-con::after{
        content:'';
        display: block;
        clear: both;
    }
    .swiper-img{
        height:100%;
        float:left;
    }
    .swiper-img a{
        display: block;
        width: 100%;
        height: 100%;
    }
    .swiper-img a .picDiv{
        width: 100%;
        height: 100%;
        background: center center no-repeat;
        background-size:cover;
    }
    .number{
        position: absolute;
        bottom:10px;
        right:10px;
        z-index: 3;
        padding:0 10px;
        border-radius: .267rem;
        background: #111;
        opacity: .5;
        color:#fff;
        strong{
            font-size:.37rem;
            font-weight: normal;
        }
        i{
            font-style: normal;
            font-size:.32rem;
        }
    }
 }
</style>