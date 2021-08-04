<template>
  <div class="slider">
      <div class="slider__main">
        <div class="slider__wrap">
            <ul ref="sliderList" class="slider__list"
              @touchstart="touchstart"
              @touchmove="touchmove"
              @touchend="touchend"
            >
              <li
                class="slider__item"
                v-for="(item, index) in sliderData"
                :key="item.title"
              >
                  <div class="slider__desc">
                    <div class="slider__pic">
                        <div class="slider__pic-num">{{ index + 1 }}</div>
                        <img :src="getImg(item)" alt="slider_photo" />
                    </div>
                    <div class="slider__subtitle">
                        {{ item.title }}
                    </div>
                    <div class="slider__text">
                        {{ item.desc }}
                    </div>
                  </div>
              </li>
            </ul>
        </div>
      </div>
      <div class="slider__btns">
          <div class="slider__btn slider__btn--prev" 
            :class="{'slider__btn--not-active': currentSlide == 0}"
            @click="slideToPrev"
          >
            <img src="../assets/icons/arrow.svg" alt="">
          </div>
          <div class="slider__btn slider__btn--next" 
            :class="{'slider__btn--not-active': currentSlide == sliderData.length - 1}"
            @click="slideToNext"
          >
            <img src="../assets/icons/arrow.svg" alt="">
          </div>
      </div>
  </div>
</template>

<script>
export default {
  name: "Slider",
  data(){
      return{
        currentSlide: 0,
        startMoveX: 0,
        startMoveY: 0,
        startTime: 0,
        endTime: 0,
        swipe: true
      }
  },
  props: {
      sliderData: {
        type: Array,
        requred: false,
      },
  },
  methods: {
      slideToPrev(){
          let vm = this
          if(vm.currentSlide > 0){
              vm.currentSlide--
              vm.$refs.sliderList.style.transform = `translateX(-${vm.currentSlide * 100}%)`
          }
      },
      slideToNext(){
          let vm = this
          if(vm.currentSlide < this.sliderData.length - 1){
              vm.currentSlide++
              vm.$refs.sliderList.style.transform = `translateX(-${vm.currentSlide * 100}%)`
          }
      },
      getImg(item){
        return item.img
      },
      touchstart(event){
          this.startMoveX = event.changedTouches[0].pageX
          this.startTime = new Date().getTime()
          this.startMoveY = event.changedTouches[0].pageY
      },
      touchmove(event){
          if(this.startMoveX < event.changedTouches[0].pageX && window.innerWidth < 768){
              this.directionFlag = true
          }else{
              this.directionFlag = false
          }
      },
      touchend(event){
          if(window.innerWidth < 768){
            let pointX = Math.abs(this.startMoveX - event.changedTouches[0].pageX)
            let pointY = Math.abs(this.startMoveY - event.changedTouches[0].pageY)
              if(pointX < pointY && pointY > 6){
                this.swipe = false
            }else{
                this.swipe = true
            }
            this.endTime = new Date().getTime()
            if(this.directionFlag){
                if(this.endTime - this.startTime > 80 && this.swipe)
                    this.slideToPrev()
            }else{
                if(this.endTime - this.startTime > 80 && this.swipe)
                    this.slideToNext()
            }
          }
      },

  },
};
</script>

