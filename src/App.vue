<template>
  <div class="wrapper">
      <div class="section slider__section">
        <div class="container">
          <h1 class="slider__title">Взгляните на процесс сборки своими глазами</h1>
          <Slider :sliderData="sliderData"></Slider>
        </div>
      </div>
      <div class="section">
        <div class="container">
            <Button
              @openModal="openModal"
            ></Button>
        </div>
      </div>
      <Modal
        v-show="modalFlag"
        @closeModal="closeModal"
      ></Modal>
  </div>
</template>

<script>
import Button from './components/Button.vue';
import Modal from './components/Modal.vue';
import Slider from "./components/Slider.vue";

export default {
 name: "App",
 components: {
  Slider,
  Button,
  Modal,
 },
 data() {
  return {
    modalFlag: false,
    sliderData: [
      {
        img: require("@/assets/image1.jpg"),
        mobImg: require("@/assets/m-img1.jpg"),
        title: "Привезём точно по списку",
        desc:" Сборщик берëт с собой наручный терминал, на котором он видит весь список покупок для каждого заказа.",
      },
      {
        img: require("@/assets/image2.jpg"),
        mobImg: require("@/assets/m-img2.jpg"),
        title: "Собираем быстро и эффективно",
        desc:"Для улучшения эргономики пространства товары размещены от тяжëлых к лëгким, находящимся уже в конечной зоне упаковки.",
      },
      {
        img: require("@/assets/image3.jpg"),
        mobImg: require("@/assets/m-img3.jpg"),
        title: "За свежесть и качество отвечаем",
        desc: "Выделены специальные зоны, в том числе холодная и морозильная.",
      },
      {
        img: require("@/assets/image4.jpg"),
        mobImg: require("@/assets/m-img4.jpg"),
        title: "Шампунь не положат рядом с рыбой",
        desc:"Собираем и упаковываем ваш заказ с заботой: соблюдаем принципы товарного соседства и учитываем вес товара.",
      },
      {
        img: require("@/assets/image5.jpg"),
        mobImg: require("@/assets/m-img5.jpg"),
        title: "Довезëм в сохранности даже яйца",
        desc:
          "Бережно транспортируем контейнеры, фиксируя их стяжными ремнями. Системы охлаждения поддерживают температурный режим.",
      },
    ],
  };
 },
 methods:{
   closeModal(){
     this.modalFlag = false
   },
   openModal(){
     this.modalFlag = true
   }
 }
};
</script>

