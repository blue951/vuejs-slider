# 适用于移动端的图片轮播组件
代码简陋但是方便加入功能。

# vuejs-slider
灵活，高度可改造。本来想做一个移动端的轮播，直接用swiper的插件就可以，但是不能实现滑动到最后一页跳转到详情的需求，所以简单实现下功能。

# 调用组件
<RrfSwiper :imgArr="swiperImg" @fatherSwiper="fatherSwiper" />
fatherSwiper(){
        this.demo2 = 1;
}
