<template>
  <div class="product-detail row">
    <div class="col-12 col-lg-8 product-detail__img">
      <div class="product-detail__img__icon" v-if="activeColor.icon">
        <img :src="activeColor.icon" alt="HIT">
      </div>
      <img :src="activeColor.productImg" :alt="kit + ' ' + title + ' ' + activeColor.title">
    </div>
    <div class="col-12 col-lg-4  product-detail__info">
      <div class="product-detail__info__title"><span>{{ kit }}</span> {{ title }} {{ activeColor.title }}</div>
      <ul class="product-detail__info__options">
        <li class="product-detail__info__option">
          <span>Цвет</span>
          <div
            class="product-detail__info__option__color"
            v-for="(color,i) in options"
            :key="i"
            @click="changeColor(i)"
            :class="{ 'active' : activeIndex === i }"
          >
            <img class="product-detail__info__option__color__img" :src="color.colorImg" :alt="color.title">
          </div>
        </li>
        <li class="product-detail__info__option"><span>Артикул</span> <strong>{{ activeColor.article }}</strong></li>
        <li class="product-detail__info__option"><span>Размер</span> <strong>{{ activeColor.size }}</strong></li>
        <li class="product-detail__info__option"><span>Вес</span> <strong>{{ activeColor.weight }}</strong></li>
        <li class="product-detail__info__option"><span>Объем</span> <strong>{{ activeColor.volume }}</strong></li>
        <li class="product-detail__info__option"><span>На складе</span> <strong>{{ activeColor.stock }}</strong></li>
        <li class="product-detail__info__option"><span>Свободно</span> <strong>{{ activeColor.free }}</strong></li>
      </ul>
      <div class="product-detail__info__controls">
        <div class="product-detail__info__controls__top-line">
          <div class="product-detail__info__controls__top-line__price">
            <div class="product-detail__info__controls__top-line__price__current">
            <span class="product-detail__info__controls__top-line__price__current__primary">
              <i class="fas fa-euro-sign"></i> {{ activeColor.price.euro | currency('', 0, {thousandsSeparator: ' '}) }}
            </span>
              <span class="product-detail__info__controls__top-line__price__current__secondary">
               <i class="fas fa-ruble-sign"></i> {{ activeColor.price.rub | currency('', 0, {thousandsSeparator: ' '}) }}
              </span>
            </div>
            <div class="product-detail__info__controls__top-line__price__old" v-show="activeColor.oldPrice">
              <span class="product-detail__info__controls__top-line__price__old__primary">
                  <i class="fas fa-euro-sign"></i> {{ activeColor.oldPrice.euro | currency('', 0, {thousandsSeparator: ' '}) }}
              </span>
              <span class="product-detail__info__controls__top-line__price__old__secondary">
                <i class="fas fa-ruble-sign"></i> {{ activeColor.oldPrice.rub | currency('', 0, {thousandsSeparator: ' '}) }}
              </span>
            </div>
          </div>
          <div class="product-detail__info__controls__top-line__actions">
            <div class="product-detail__info__controls__top-line__action__counter">
              <input type="hidden" :value="counterValue" name="counter" class="product-detail-counter-value">
              <el-input-number :min="1" :max="activeColor.free" :name="counterName" v-model="counterValue"></el-input-number>
            </div>
            <div class="product-detail__info__controls__top-line__actions__buy">
              <slot name="buy">
                <small>Тут кнопка положить в корзину</small>
              </slot>
            </div>
          </div>
        </div>
        <div class="product-detail__info__controls__bottom-line">
          <slot name="buy-one-click">
            <small>Тут кнопка быстрой покупки</small>
          </slot>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      title: {
        default: 'СТОЛ L160'
      },
      kit: {
        default: 'FERMO WOOD'
      },
      counterName: {
        default: 'product-detail-counter'
      },
      options: {
        default: function () {
          return [
              {
                title: 'ВЕНГЕ',
                colorImg: 'assets/img/product-detail/color-1.jpg',
                productImg: 'assets/img/product-detail/img-1.jpg',
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
                productImg: 'assets/img/product-detail/img-2.jpg',
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
                productImg: 'assets/img/product-detail/img-3.jpg',
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
  .product-detail {
    &__img {
      position: relative;
      display: flex;
      justify-content: center;
      align-items: center;
      &__icon {
        top: 15px;
        left: 20px;
        position: absolute;
      }
      img {
        width: auto;
        height: auto;
        max-width: 100%;
      }
    }
    &__info {
      &__controls {

        &__top-line {
          display: flex;
          @media all and (max-width: $mdDesktopWidth) and (min-width: $smDesktopWidth) {
            flex-wrap: wrap;
            &__price {
              margin-bottom: 20px;
            }
          }
          @media all and (max-width: $phoneWidth) {
            flex-wrap: wrap;
            &__price {
              margin-bottom: 20px;
            }
          }
          align-items: center;
          background-color: #4e4e4e;
          padding: 20px;
          &__actions {
            flex: 1 1 50%;
            @media all and (max-width: $phoneWidth) {
              padding-left: 0;
            }
            padding-left: 20px;
            flex-wrap: nowrap;
            display: flex;
            justify-content: space-between;
            align-items: center;
            min-width: 200px;
            &__buy {
              flex: 1 1 50%;
            }
            &__counter {
              flex: 1 1 50%;
            }

          }
          &__price {
            flex: 1 1 50%;
            display: flex;
            align-items: center;
            justify-content: space-between;
            &__old {
              &__primary {
                position: relative;
                font-size: 15px;
                display: block;
                color: $primary-color;
                font-weight: 300;
              }
              &__secondary {
                position: relative;
                font-size: 13px;
                display: block;
                color: #aaaaab;
                font-weight: 300;
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
            &__current {
              &__primary {
                font-size: 30px;
                color: $primary-color;
                font-weight: 700;
                display: block;
              }
              &__secondary {
                font-size: 20px;
                color: #aaaaab;
                font-weight: 400;
                display: block;
              }
            }
          }
        }
        &__bottom-line {
          padding: 20px;
          display: flex;
          align-items: center;
          justify-content: flex-end;
        }

      }
      &__title {
        text-transform: uppercase;
        color: #000;
        font-size: 23px;
        font-weight: 700;
        margin-bottom: 50px;
        span {
          color: $primary-color;
        }
      }
      &__options {
        margin-bottom: 100px;
      }
      &__option {
        display: flex;
        align-items: center;
        margin-bottom: 16px;
        span {
          display: block;
          margin-right: 8px;
          text-transform: uppercase;
          color: #bfbfbf;
          font-weight: 700;
        }
        strong {
          color: #000;
          text-transform: uppercase;
        }

        &__color.active {
          img {
            border: 1px solid red;
          }

        }

        &__color {
          padding: 0 5px;
          &__img {
            border-radius: 3px;
            width: 31px;
            height: 31px;
          }
        }
      }
    }
  }
  .product-detail__info__controls__top-line__action__counter {
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
    .el-input-number .el-input__inner {
      border-color: transparent;
      padding-left: 10px;
      padding-right: 10px;
      border-radius: 0;
    }
  }
</style>