<template>
  <div class="base-slider-1">
    <div class="base-slider-1_slide_information_modal">
      <sweet-modal title="Оформление заказа" ref="order">
        <form class="form-order" @submit.prevent="formSumbit">
          <input type="text" name="name" placeholder="Введите ваше имя">
          <input type="tel" name="phone" placeholder="Укажите номер телефона">
          <input type="email" name="email" placeholder="Введите свою почту">
          <textarea type="text" name="message" placeholder="Задавайте любые вопросы"></textarea>
          <div class="d-flex justify-content-around align-items-center my-2">
            <button type="submit" class="btn btn-default">Заказать</button>
          </div>
        </form>
      </sweet-modal>
      <sweet-modal icon="success" ref="success">
        Вашая заявка успешно обработана, вскоре с вами свяжуться наши менеджеры.
      </sweet-modal>
    </div>
    <carousel
        :per-page="1"
        pagination-active-color="#f0ad19"
        pagination-color="#fff"
        navigation-prev-label='<i class="fas fa-chevron-left"></i>'
        navigation-next-label='<i class="fas fa-chevron-right"></i>'
        :pagination-enabled="true"
        :navigation-enabled="true">
      <slide class="base-slider-1_slide" v-for="(slide, index) in sliderData" :key="index">
          <div class="base-slider-1_slide_img">
            <img :src="slide.img" :alt="slide.title">
          </div>
          <div class="base-slider-1_slide_information">
            <vue-tabs>
              <v-tab :title="tabItem.tab" v-for="(tabItem, i) in slide.content" :key="i">
                <div class="base-slider-1_slide_information_header">
                  <h3 class="base-slider-1_slide_information_title">{{ tabItem.title }}</h3>
                  <div class="base-slider-1_slide_information_space">
                    <span>{{ tabItem.value }}</span> м2
                  </div>
                </div>
                <div class="base-slider-1_slide_information_content" v-html="tabItem.text"></div>
                <div class="d-flex justify-content-around align-items-center">
                  <button class="btn btn-default m-0" @click="$refs.order.open()">Оформить заказ</button>
                </div>
              </v-tab>
            </vue-tabs>
            <div class="base-slider-1_slide_information_footer">
              <span>Ипотека</span>
              <i class="fas fa-calculator"></i>
              <i class="far fa-star"></i>
            </div>
          </div>
      </slide>
    </carousel>
  </div>
</template>

<script>
export default {
  data() {
    return {
      sliderData: [
        {
          img: 'assets/img/index/pomestie-3.jpg',
          alt: 'Slide 1',
          content: [
            {
              tab: 'Все проекты',
              title: 'Франкфурт',
              value: '93',
              text: `
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
              `
            },
            // {
            //   tab: 'Готовые продукты',
            //   title: 'Франкфурт',
            //   value: '93',
            //   text: `
            //       <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
            //       <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
            //       <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
            //       <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
            //       <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
            //   `
            // }
          ],
        },
        {
          img: 'assets/img/index/06d7c1e3ff9bc75cc9d0fa93d9f3f1b8.jpg',
          alt: 'Slide 1',
          content: [
            {
              tab: 'Все проекты',
              title: 'Франкфурт',
              value: '93',
              text: `
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
              `
            },
            {
              tab: 'Готовые продукты',
              title: 'Франкфурт',
              value: '93',
              text: `
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
              `
            }
          ],
        },
        {
          img: 'assets/img/index/1-46.jpg',
          alt: 'Slide 1',
          content: [
            {
              tab: 'Все проекты',
              title: 'Франкфурт',
              value: '93',
              text: `
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
              `
            },
            {
              tab: 'Готовые продукты',
              title: 'Франкфурт',
              value: '93',
              text: `
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
              `
            }
          ],
        },
        {
          img: 'assets/img/index/1-17.jpg',
          alt: 'Slide 1',
          content: [
            {
              tab: 'Все проекты',
              title: 'Франкфурт',
              value: '93',
              text: `
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
              `
            },
            {
              tab: 'Готовые продукты',
              title: 'Франкфурт',
              value: '93',
              text: `
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
              `
            }
          ],
        },
        {
          img: 'assets/img/index/000.jpg',
          alt: 'Slide 1',
          content: [
            {
              tab: 'Все проекты',
              title: 'Франкфурт',
              value: '93',
              text: `
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
              `
            },
            {
              tab: 'Готовые продукты',
              title: 'Франкфурт',
              value: '93',
              text: `
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus alias at corporis cupiditate expedita laboriosam, maiores omnis perferendis quibusdam sit.</p>
              `
            }
          ],
        },
      ]
    }
  },
  methods: {
    formSumbit() {
      this.$refs.order.close()
      this.$refs.success.open()
    }
  }
}
</script>

<style lang="scss">
@import "../scss/utils/vars.scss";
.base-slider-1_slide_information_modal {}
.form-order {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 35px;
  input {
    width: 100%;
    font-size: 18px;
    line-height: 1.4;
    padding: 8px 12px;
    border: 1px solid $primary-color;
    margin-bottom: 15px;
  }
  textarea {
    width: 100%;
    font-size: 16px;
    border: 1px solid $primary-color;
    line-height: 1;
    padding: 15px;
    margin-bottom: 15px;
  }
}
.base-slider-1 {
  &_slide {
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    height: 600px;
  }
  &_slide_img {
    flex: 0 0 63%;
  }
  &_slide_information {
    flex: 0 0 37%;
    display: flex;
    flex-direction: column;
    height: 100%;
    background-color: $secondary-color;
  }
  .vue-tabs {
    padding: 23px 31px;
  }
  &_slide_information_header {
    color: #000000;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 30px 0;
  }
  &_slide_information_title {
    font-family: $mainFont;
    font-size: 30px;
    font-weight: 300;
    line-height: 2;
  }
  &_slide_information_space {
    font-family: $secondFont;
    font-size: 30px;
    font-weight: 700;
    color: #000;
    span {
      font-size: 44px;
      color: $primary-color;
    }
  }
  &_slide_information_content {
    overflow-y: auto;
    max-height: 260px;
    margin-bottom: 27px;
  }
  &_slide_information_footer {
    font-family: $secondFont;
    font-size: 15px;
    font-weight: 400;
    text-transform: uppercase;
    letter-spacing: 1.13px;
    color: $default-color;
    display: flex;
    align-items: center;
    background-color: #464646;
    min-height: 60px;
    padding: 10px 20px;
    margin-top: auto;
    i {
      font-size: 21px;
      margin-left: 24px;
    }
    .fa-star {
      margin-left: auto;
      color: $primary-color;
    }
  }
  .VueCarousel-navigation-prev {
    z-index: 10;
    left: -20px;
    @media screen and (max-width: 1400px) {
      left: 30px;
    }
  }
  .VueCarousel-navigation-next {
    z-index: 10;
    right: -20px;
    @media screen and (max-width: 1400px) {
      right: 30px;
    }
  }
  .VueCarousel-pagination {
    width: 63%;
    margin-top: -75px;
    z-index: 2;
  }
  .VueCarousel-dot {
    border-radius: 1px;
  }
}
</style>
