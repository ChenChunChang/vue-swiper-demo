
<template>
  <div class="thumb-example" @mouseover="mouseover" @mouseout="mouseout">
    <!-- swiper1 -->
    <swiper ref="swiperTop" class="swiper gallery-top" :options="swiperOptionTop">
      <swiper-slide class="slide-1"></swiper-slide>
      <swiper-slide class="slide-2"></swiper-slide>
      <swiper-slide class="slide-3"></swiper-slide>
      <swiper-slide class="slide-4"></swiper-slide>
      <swiper-slide class="slide-5"></swiper-slide>
      <div slot="button-next" class="swiper-button-next swiper-button-white"></div>
      <div slot="button-prev" class="swiper-button-prev swiper-button-white"></div>
    </swiper>
    <!-- swiper2 Thumbs -->
    <swiper ref="swiperThumbs" class="swiper gallery-thumbs" :options="swiperOptionThumbs">
      <swiper-slide class="slide-1"></swiper-slide>
      <swiper-slide class="slide-2"></swiper-slide>
      <swiper-slide class="slide-3"></swiper-slide>
      <swiper-slide class="slide-4"></swiper-slide>
      <swiper-slide class="slide-5"></swiper-slide>
    </swiper>
  </div>
</template>

<script>
export default {
  components: {
  },
  data() {
    return {
      swiperOptionTop: {
        loop: true,
        loopedSlides: 5, // looped slides should be the same
        spaceBetween: 10,
        autoplay: {
          delay: 2500,
          // pauseOnMouseEnter: true,
          disableOnInteraction: false
        },
        navigation: {
          nextEl: '.swiper-button-next',
          prevEl: '.swiper-button-prev'
        }
      },
      swiperOptionThumbs: {
        loop: true,
        loopedSlides: 5, // looped slides should be the same
        spaceBetween: 10,
        centeredSlides: true,
        slidesPerView: 'auto',
        touchRatio: 0.2,
        slideToClickedSlide: true
      }
    }
  },
  mounted() {
    this.$nextTick(() => {
      const swiperTop = this.$refs.swiperTop.swiper
      const swiperThumbs = this.$refs.swiperThumbs.swiper
      swiperTop.controller.control = swiperThumbs
      swiperThumbs.controller.control = swiperTop
    })
  },
  methods: {
    mouseover() {
      this.$refs.swiperTop.swiper.autoplay.stop()
    },
    mouseout() {
      this.$refs.swiperTop.swiper.autoplay.start()
    }
  }
}
</script>

<style lang="less" scoped>
.thumb-example {
  width: 800px;
  height: 480px;
  margin: 0 auto;
  background: #000;
  //background-color: $black;
}

.swiper {
  .swiper-slide {
    background-size: cover;
    background-position: center;

    &.slide-1 {
      background-image:url('https://github.surmon.me/images/example/1.jpg');
    }
    &.slide-2 {
      background-image:url('https://github.surmon.me/images/example/2.jpg');
    }
    &.slide-3 {
      background-image:url('https://github.surmon.me/images/example/4.jpg');
    }
    &.slide-4 {
      background-image:url('https://github.surmon.me/images/example/5.jpg');
    }
    &.slide-5 {
      background-image:url('https://github.surmon.me/images/example/6.jpg');
    }
  }

  &.gallery-top {
    height: 80%;
    width: 100%;
  }
  &.gallery-thumbs {
    height: 20%;
    box-sizing: border-box;
    //padding: $gap 0;
  }
  &.gallery-thumbs .swiper-slide {
    width: 25%;
    height: 100%;
    opacity: 0.4;
  }
  &.gallery-thumbs .swiper-slide-active {
    opacity: 1;
  }
}
</style>
