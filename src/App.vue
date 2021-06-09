<template>
  <div id="app" class="app">
    <h2 class="title">Взгляните на процесс сборки своими глазами</h2>
    <carousel
        @next="next"
        @prev="prev"
    >
      <slide
          v-for="(slide, idx) in slides"
          :key="idx"
          :curent="idx"
          :visibleSlide="visible"
          :direction="direction"
          class="carousel-slider"
      >
        <div class="carousel-slider__item">
          <div class="carousel-slider__img">
            <img :src="slide.img" alt="">
            <div class="carousel-slider__curent">{{ idx + 1 }}</div>
          </div>
          <h6 class="title__h6">{{ slide.title }}</h6>
          <p class="carousel-slider__article">
            {{ slide.article }}
          </p>
        </div>
      </slide>
    </carousel>

    <button class="btn__buy" @click="popup = !popup">К покупкам</button>
    <popup :toggle="popup" @close="close"></popup>
  </div>
</template>

<script>
  import Carousel from "./components/Carousel/Carousel";
  import Slide from "./components/Carousel/Slide";
  import Popup from "./components/Popup/Popup"

  export default {
    data() {
      return {
        slides: [
          {
            img: require('./assets/img/i1.jpg'),
            title: 'Привезём точно по списку',
            article: 'Сборщик берëт с собой наручный терминал, на котором он видит весь список покупок для каждого заказа.'
          },
          {
            img: require('./assets/img/i2.jpg'),
            title: 'Собираем быстро и эффективно',
            article: 'Для улучшения эргономики пространства товары размещены от тяжëлых к лëгким, находящимся уже в конечной зоне упаковки.'
          },
          {
            img: require('./assets/img/i3.jpg'),
            title: 'За свежесть и качество отвечаем',
            article: 'Выделены специальные зоны, в том числе холодная и морозильная.'
          },
          {
            img: require('./assets/img/i4.jpg'),
            title: 'Шампунь не положат рядом с рыбой',
            article: 'Собираем и упаковываем ваш заказ с заботой: соблюдаем принципы товарного соседства и учитываем вес товара.'
          },
          {
            img: require('./assets/img/i5.jpg'),
            title: 'Довезëм в сохранности даже яйца',
            article: 'Бережно транспортируем контейнеры, фиксируя их стяжными ремнями. Системы охлаждения поддерживают температурный режим.'
          },
        ],
        visible: 0,
        direction: 'left',
        popup: false,
      }
    },
    methods: {
      next() {
        if (this.visible >= this.slLength - 1) {
          this.visible = 0
        } else {
          this.visible++
        }
        this.direction = "left"
      },
      prev() {
        if (this.visible <= 0) {
          this.visible = this.slLength - 1
        } else {
          this.visible--
        }
        this.direction = "right"
      },
      close() {
        this.popup = false
      }
    },
    computed: {
      slLength() {
        return this.slides.length
      }
    },
    components: {
      Carousel,
      Slide,
      Popup
    }
  }
</script>

<style lang="scss">
  @import "assets/scss/styles.scss";
  @import "assets/scss/popup.scss";
</style>
