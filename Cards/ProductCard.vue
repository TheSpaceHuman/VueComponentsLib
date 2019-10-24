<template>
  <figure class="product-card">
      <div class="product-card__img">
        <img :src="activeColor.productImg" :alt="title">
        <div class="product-card__img__icon" v-if="activeColor.icon">
          <img :src="activeColor.icon" alt="HIT">
        </div>
      </div>
      <div class="product-card__content">
        <h4 class="product-card__content__title">
          <strong>{{ kit }}</strong> {{ title }} {{ activeColor.title }}
        </h4>
        <div class="product-card__content__options">
          <ul class="product-card__content__options__items">
            <li class="product-card__content__options__item">
              <strong>Артикул</strong>
              <span>{{ activeColor.article }}</span>
            </li>
            <li class="product-card__content__options__item">
              <strong>Размер</strong>
              <span>{{ activeColor.size }}</span>
            </li>
            <li class="product-card__content__options__item option--color">
              <strong>Цвет</strong>
              <div class="product-card__content__options__item__color-list">
                <div
                  class="product-card__content__options__item__color-item"
                  v-for="(color,i) in options"
                  :key="i"
                  @click="changeColor(i)"
                  :class="{ 'active' : activeIndex === i }"
                >
                  <img class="product-card__content__options__item__color-item__img" :src="color.colorImg" :alt="color.title">
                </div>
              </div>
            </li>

            <li class="product-card__content__options__item">
              <strong>На складе</strong>
              <span>{{ activeColor.stock }}</span>
            </li>
            <li class="product-card__content__options__item">
              <strong>Свободно</strong>
              <span>{{ activeColor.free }}</span>
            </li>
          </ul>
        </div>
      </div>
      <div class="product-card__bottom">
        <div class="product-card__bottom__price">
          <div class="product-card__bottom__price__main">
            <span class="product-card__bottom__price__main__primary">
              <i class="fas fa-euro-sign"></i> {{ activeColor.price.euro | currency('', 0, {thousandsSeparator: ' '}) }}
            </span>
            <span class="product-card__bottom__price__main__secondary">
              <i class="fas fa-ruble-sign"></i> {{ activeColor.price.rub | currency('', 0, {thousandsSeparator: ' '}) }}
            </span>
          </div>
          <div class="product-card__bottom__price__old">
            <span class="product-card__bottom__price__old__primary">
               <i class="fas fa-euro-sign"></i> {{ activeColor.oldPrice.euro | currency('', 0, {thousandsSeparator: ' '}) }}
            </span>
            <span class="product-card__bottom__price__old__secondary">
              <i class="fas fa-ruble-sign"></i> {{ activeColor.oldPrice.rub | currency('', 0, {thousandsSeparator: ' '}) }}
            </span>
          </div>
        </div>
        <div class="product-card__bottom__actions">
          <div class="product-card__bottom__actions__counter">
            <input type="hidden" :value="counterValue" name="counter" class="product-card-counter-value">
            <el-input-number :min="1" :max="activeColor.free" :name="counterName" v-model="counterValue"></el-input-number>
          </div>
          <div class="product-card__bottom__actions__buy">
            <slot name="buy">
              <small>Тут кнопка положить в корзину</small>
            </slot>
          </div>
        </div>
      </div>
  </figure>
</template>

<script>
  export default {
    name: 'ProductCard',
    props: {
      title: {
        default: 'СТОЛ L160'
      },
      kit: {
        default: 'FERMO WOOD'
      },
      counterName: {
        default: 'product-card-counter'
      },
      options: {
        default: function () {
          return [
            {
              title: 'ВЕНГЕ',
              colorImg: 'assets/img/product-detail/color-1.jpg',
              productImg: 'assets/img/product-collection/product-1.jpg',
              article: '41S002 V3V2',
              size: '160 x 90 x h75 см',
              weight: '72',
              volume: '0.098',
              stock: 13,
              free: 8,
              price: {
                rub: 120000,
                euro: 1600
              },
              oldPrice: {
                rub: 130375,
                euro: 1781
              },
              icon: ''
            },
            {
              title: 'ДУБ DH СВЕТЛЫЙ',
              colorImg: 'assets/img/product-detail/color-2.png',
              productImg: 'assets/img/product-collection/product-2.jpg',
              article: '82S002 V3V2',
              size: '160 x 90 x h75 см',
              weight: '72',
              volume: '0.098',
              stock: 12,
              free: 5,
              price: {
                rub: 110000,
                euro: 1500
              },
              oldPrice: {
                rub: 130375,
                euro: 1781
              },
              icon: ''
            },
            {
              title: 'ДУБ СВЕТЛЫЙ',
              colorImg: 'assets/img/product-detail/color-3.png',
              productImg: 'assets/img/product-collection/product-3.jpg',
              article: '723S002 V3V2',
              size: '160 x 90 x h75 см',
              weight: '72',
              volume: '0.098',
              stock: 79,
              free: 55,
              price: {
                rub: 100000,
                euro: 1550
              },
              oldPrice: {
                rub: 110375,
                euro: 1681
              },
              icon: 'assets/img/index/sale-icon.png'
            },
          ]
        }
      }
    },
    data() {
      return {
        activeIndex: 0,
        counterValue: 1
      }
    },
    computed: {
      activeColor() {
        return this.options[this.activeIndex]
      }
    },
    methods: {
      changeColor(index) {
        return this.activeIndex = index
      }
    },
    watch: {
      activeColor: function (newValue, oldValue) {
        if(newValue.free < oldValue.free) {
          this.counterValue = newValue.free
        }
      }
    }
  }
</script>

<style lang="scss">
  @import "../scss/utils/vars";
  .product-card {
    padding: 8px;
    background-color: #f8f5f2;
    margin: 0 0 50px;

    &__bottom {
      padding: 20px;
      background-color: #fff;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;

      &__price {
        flex: 1 1 50%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        &__main {
          flex: 0 0 70%;
          &__primary {
            font-size: 30px;
            color: $primary-color;
            font-weight: 700;
            display: block;
            white-space: nowrap;
          }
          &__secondary {
            font-size: 20px;
            color: #aaaaab;
            font-weight: 400;
            display: block;
            white-space: nowrap;
          }
        }
        &__old {
          flex: 0 0 30%;
          &__primary {
            position: relative;
            font-size: 15px;
            display: block;
            color: $primary-color;
            font-weight: 300;
            white-space: nowrap;
          }
          &__secondary {
            position: relative;
            font-size: 13px;
            display: block;
            color: #aaaaab;
            font-weight: 300;
            white-space: nowrap;
          }
          &__primary::before {
            position: absolute;
            content: '';
            width: 100%;
            height: 1px;
            background-color: $primary-color;
            top: 50%;
          }
          &__secondary::before {
            position: absolute;
            top: 50%;
            content: '';
            width: 100%;
            height: 1px;
            background-color: #aaaaab;
          }
        }
      }
      &__actions > div {
        flex: 1 1 auto;
      }
      &__actions {
        flex: 1 1 50%;
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding-left: 20px;
        @media screen and (min-width: $tableWidth) and (max-width: $mdDesktopWidth) {
          padding-top: 12px;
          padding-left: 0;
        }
        @media screen and (min-width: $phoneWidth) and (max-width: $tableWidth) {
          padding-top: 0;
          padding-left: 20px;
        }
        @media screen and (max-width: $phoneWidth) {
          padding-left: 0;
        }
        &__buy {
          button, a {
            width: 100%;
          }
        }
      }
    }
    &__img > img {
      width: 100%;
    }
    &__img {
      position: relative;

      &__icon {
        position: absolute;
        top: 20px;
        left: 20px;
      }
    }
    &__content {

      &__title {
        text-transform: uppercase;
        font-weight: 700;
        font-size: 18px;
        color: #000000;
        padding: 12px 18px;
        border-bottom: 1px solid #bfbfbf;
        margin-bottom: 10px;
        strong {
          color: $primary-color;
        }
      }
      &__options {
        padding: 8px 18px;
        &__items {
          display: flex;
          flex-wrap: wrap;
        }
        &__item.option--color {
          flex: 0 0 100%;
          display: flex;
          align-items: center;
        }
        &__item {
          flex: 0 0 50%;
          text-transform: uppercase;
          font-size: 14px;
          font-weight: 700;
          color: #000;
          margin-bottom: 12px;
          strong {
            color: #bfbfbf;
          }
          span {
            font-weight: 700;
          }

          &__color-list {
            display: flex;
          }
          &__color-item.active {
            border: 1px solid red;
          }
          &__color-item {
            margin: 0 5px;

            img {
              width: 24px;
              height: 24px;
            }
          }

        }
      }
    }
  }
  .product-card__bottom__actions__counter {
    display: flex;
    justify-content: center;
    .el-icon-minus::before {
      font-family: "Font Awesome 5 Free";
      font-weight: 900;
      content: "\f053";
      /*color: #fff;*/
    }
    .el-icon-plus::before {
      font-family: "Font Awesome 5 Free";
      font-weight: 900;
      content: "\f054";
      /*color: #fff;*/
    }
    .el-input-number {
      background-color: #bfbfbf;
      border-color: #bfbfbf;
      border-radius: 0;
    }
    .el-input-number__decrease.is-disabled, .el-input-number__increase.is-disabled {
      color: rgba(255,255,255, 0.4);
    }

    .el-input-number__decrease, .el-input-number__increase {
      background-color: transparent;
      border-color: transparent;
      border-radius: 0;
      color: #fff;
    }
    .el-input-number {
      width: 100%;
    }
    .el-input__inner {
      min-width: 80px;
    }
    .el-input-number .el-input__inner {
      border-color: transparent;
      padding-left: 10px;
      padding-right: 10px;
      border-radius: 0;
    }
  }
</style>