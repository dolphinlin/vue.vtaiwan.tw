<template lang="jade">

  .component

    #loader.ui.active.inverted.dimmer
      .ui.loader

    .swiper-container
      .swiper-scrollbar
      .swiper-pagination 
      .swiper-wrapper
        .swiper-slide(v-for="(item, idx) in hotTopics", :style="{'background': 'url(' + item.cover + ') 100% 100% / cover'}")
          .box
            .status.ui.basic.huge.label 
              | {{item.status}}
            h1.slogan.ui.center.aligned.header
              | {{item.title}}
              .sub.center.aligned.header
                | {{item.slogan}}
            router-link.go-inside.ui.right.labeled.icon.teal.big.button(:to="'/topic/' + item.routeName")
              i.right.arrow.icon
              p 進入議題
            //- i.square.icon.background
            button.go-to.ui.yellow.vertical.animated.button(@click="goAnchor('#proposaltab')")
              .hidden.content
                | 還有更多議案
              .visible.content
                i.down.arrow.icon
      
</template>


<script>

export default {
  name: 'SlideShow',
  props: ['hotTopics', 'allTopics'],
  data () {
    return {
    }
  },
  methods: {
    goAnchor: function(anchor){
      if(anchor == "top"){
        /* go to top */
        $('html, body').animate({
          scrollTop: 0,
        }, 1000)
      }
      else if(anchor){
        /* get the top position of anchor */
        let anchor_y = $(anchor).offset().top
        /* go to anchor (animation to do) */
        $('html, body').animate({
          scrollTop: anchor_y,
        }, 1000)
      }
    }
  },
  mounted: function () {

    setTimeout(function(){
      /* initialize swiper when document ready */
      new Swiper ('.swiper-container', {
        observer: true,
        scrollbar: '.swiper-scrollbar',
        pagination : '.swiper-pagination',
        autoplay: 8000,
        direction: 'horizontal',
        keyboardControl: true,
        slidesPerView: 1.2,
        centeredSlides: true,
        spaceBetween: 20,
        paginationClickable :true,
        loop: true,
        grabCursor: true
      })
      /* disable loader */
      $('#loader').removeClass('active')
    }, 1000)

  }
}

</script>

<style lang="scss" scoped>
@import "../sass/global.scss";

// ******************************* Swiper slide

.component {
  height: 100vh;
  @media only screen and (max-width: $breakpoint) {
    height: 100vh - $m-navHeight;
  }
  padding: 0 0 1em 0;
}

.swiper-container {
  height: 100%;
}

// ******************************* Desktop CSS

.ui.label{
  border-radius: 0;
}

.box {
  // font-size: 1rem;
  // ********************* centering
  display: flex;
  justify-content: center;
  flex-flow: column;
  align-items: center;
  // ********************* 
  width: 100%;
  height: 100%;
  background: radial-gradient(circle, rgba(0,0,0, 0.7), rgba(0,0,0, 0.5));
  overflow: hidden;
  .status, .status[data-v-5122aa90]{
    radius: 0px;
    color: white;
    background: rgba(255,255,255,0.4);
    border: 0px;
    font-size: 1.2rem;  
  },
  .status,
  .title,
  .slogan,
  .go-inside {
    z-index: 10;
  }
  .status {
    color: $step_color;
    border: 1px solid $step_color;
    background: transparent;
  }
  .title {
    color: white;
  }
  .slogan {
    margin: .5em 0;
    font-size: 3rem;
    @media only screen and (max-width: $breakpoint) {
      font-size: 2rem;
    }
    .sub.header {
      color: white;
      margin: 10px;
    }
    color: white;
  }
  .go-inside {
    margin: 0 0 1em 0;
  }
  .go-to {
    width: 20ch;
    position: absolute;
    bottom: 3em;
    font-family: $main_font;
    font-size: 60%;
  }
}

</style>