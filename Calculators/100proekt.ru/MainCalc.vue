<template>
  <div class="main-calc-wrapper">
    <div class="row">
      <div class="col-12">
        <small class="calc-step">Шаг 1</small>
        <b-form-group label="Длина" horizontal>
          <b-form-input
            v-model.number="inputData.long"
            placeholder="В метрах"
            @keydown="changeDown"
            @focus="clearInput"
          ></b-form-input>
        </b-form-group>
        <small class="calc-step">Шаг 2</small>
        <b-form-group label="Ширина" horizontal>
          <b-form-input
            v-model.number="inputData.width"
            placeholder="В метрах"
            @keydown="changeDown"
            @focus="clearInput"
          ></b-form-input>
        </b-form-group>
        <b-form-group label="Строительная площадь" horizontal><span class="main-calc-wrapper__computed-value">{{ buildingArea | currency(' м	&sup2;', 2, { symbolOnLeft: false }) }}</span></b-form-group>
        <b-form-group label="Площадь фасада" horizontal><span class="main-calc-wrapper__computed-value">{{ facadeArea | currency(' м	&sup2;', 2, { symbolOnLeft: false }) }}</span></b-form-group>
        <b-form-group label="Площадь окон " horizontal><span class="main-calc-wrapper__computed-value">{{ windowArea | currency(' м	&sup2;', 2, { symbolOnLeft: false }) }}</span></b-form-group>
        <small class="calc-step">Шаг 3</small>
        <div class="main-calc-wrapper__radio-label-list">
          <label class="main-calc-wrapper__radio-label-item" :class="{'active' : inputData.area === '1'}">
            <img src="https://simferopol.virmak.ru/local/templates/zukka/img/calculator/1.png" alt="Один этаж без мансарды">
            <b-form-radio v-model="inputData.area" name="area" value="1">Один этаж без мансарды</b-form-radio>
          </label>
          <label class="main-calc-wrapper__radio-label-item" :class="{'active' : inputData.area === '1-M'}">
            <img src="https://simferopol.virmak.ru/local/templates/zukka/img/calculator/2.png" alt="Один этаж с мансардой">
            <b-form-radio v-model="inputData.area" name="area" value="1-M">Один этаж с мансардой</b-form-radio>
          </label>
          <label class="main-calc-wrapper__radio-label-item" :class="{'active' : inputData.area === '2'}">
            <img src="https://simferopol.virmak.ru/local/templates/zukka/img/calculator/3.png" alt="Два полных этажа">
            <b-form-radio v-model="inputData.area" name="area" value="2">Два полных этажа</b-form-radio>
          </label>
          <label class="main-calc-wrapper__radio-label-item" :class="{'active' : inputData.area === '2-M'}">
            <img src="https://simferopol.virmak.ru/local/templates/zukka/img/calculator/4.png" alt="Два этажа с мансардой">
            <b-form-radio v-model="inputData.area" name="area" value="2-M">Два этажа с мансардой</b-form-radio>
          </label>
          <label class="main-calc-wrapper__radio-label-item" :class="{'active' : inputData.area === '3'}">
            <img src="https://simferopol.virmak.ru/local/templates/zukka/img/calculator/5.png" alt="Три полных этажа">
            <b-form-radio v-model="inputData.area" name="area" value="3">Три полных этажа</b-form-radio>
          </label>
          <label class="main-calc-wrapper__radio-label-item" :class="{'active' : inputData.area === '3-M'}">
            <img src="https://simferopol.virmak.ru/local/templates/zukka/img/calculator/6.png" alt="Три этажа с мансардой">
            <b-form-radio v-model="inputData.area" name="area" value="3-M">Три этажа с мансардой</b-form-radio>
          </label>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-8">
        <small class="calc-step">Шаг 4</small>
        <b-form-group :label="options.foundation.title" horizontal>
          <b-form-select v-model="options.foundation.value" :options="options.foundation.items"></b-form-select>
        </b-form-group>
      </div>
      <div class="col-4"><div class="main-calc-wrapper__service-value">{{ foundationCalc | currency(' ₽', 2, { symbolOnLeft: false, thousandsSeparator: ' ' }) }}</div></div>

      <div class="col-8">
        <small class="calc-step">Шаг 5</small>
        <b-form-group :label="options.material.title" horizontal>
          <b-form-select v-model="options.material.value" :options="options.material.items"></b-form-select>
        </b-form-group>
      </div>
      <div class="col-4"><div class="main-calc-wrapper__service-value">{{ materialCalc | currency(' ₽', 2, { symbolOnLeft: false, thousandsSeparator: ' ' }) }}</div></div>

      <div class="col-8">
        <small class="calc-step">Шаг 6</small>
        <b-form-group :label="options.interfloorOverlap.title" horizontal>
          <b-form-select v-model="options.interfloorOverlap.value" :options="options.interfloorOverlap.items"></b-form-select>
        </b-form-group>
      </div>
      <div class="col-4"><div class="main-calc-wrapper__service-value">{{ interfloorOverlapCalc | currency(' ₽', 2, { symbolOnLeft: false, thousandsSeparator: ' ' }) }}</div></div>

      <div class="col-8">
        <small class="calc-step">Шаг 7</small>
        <b-form-group :label="options.roof.title" horizontal>
          <b-form-select v-model="options.roof.value" :options="options.roof.items"></b-form-select>
        </b-form-group>
      </div>
      <div class="col-4"><div class="main-calc-wrapper__service-value">{{ roofCalc | currency(' ₽', 2, { symbolOnLeft: false, thousandsSeparator: ' ' }) }}</div></div>

      <div class="col-8">
        <small class="calc-step">Шаг 8</small>
        <b-form-group :label="options.facadeDecoration.title" horizontal>
          <b-form-select v-model="options.facadeDecoration.value" :options="options.facadeDecoration.items"></b-form-select>
        </b-form-group>
      </div>
      <div class="col-4"> <div class="main-calc-wrapper__service-value">{{ facadeDecorationCalc | currency(' ₽', 2, { symbolOnLeft: false, thousandsSeparator: ' ' }) }}</div></div>

      <div class="col-8">
        <small class="calc-step">Шаг 9</small>
        <b-form-group :label="options.window.title" horizontal>
          <b-form-select v-model="options.window.value" :options="options.window.items"></b-form-select>
        </b-form-group>
      </div>
      <div class="col-4"><div class="main-calc-wrapper__service-value">{{ windowCalc | currency(' ₽', 2, { symbolOnLeft: false, thousandsSeparator: ' ' }) }}</div></div>
    </div>
    <div class="row">
      <div class="col-12">
        <small class="calc-step">Шаг 10</small>
        <div class="d-flex align-items-center justify-content-center pt-3 mb-5">
          <b-button variant="danger" @click="allCalc">Рассчитать стоимость дома</b-button>
        </div>
        <div class="main-calc-wrapper__result-wrapper" v-if="result">
          <h5 class="main-calc-wrapper__result-value">Итоговая стоимость строительства: {{ result | currency(' ₽', 2, { symbolOnLeft: false, thousandsSeparator: ' ' }) }}</h5>
          <h5 class="main-calc-wrapper__result-area">Стоимость 1 м&sup2; : {{ resultArea | currency(' ₽', 2, { symbolOnLeft: false, thousandsSeparator: ' ' }) }}</h5>
          <p class="main-calc-wrapper__result-descriptions">{{ descriptions }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "MainCalc",
    props: {
      domain: {
        default: ''
      },
      descriptions: {
        type: String,
        default: 'Данный список работ и материалов может корректироваться в зависимости от специфики конкретного объекта и желаний заказчика. Окончательная цена строительства дома складывается из многих факторов: общей площади и числа помещений, стоимости материалов, исходной сложности работ, специфики рельефа, геологии участка, сейсмичности площадки, стесненных условий строительства  и т.д. Имеет значение и сложность архитектурной формы: наличие фигурных элементов, нестандартность планировки и т.д. Порой в процессе воплощения отдельных задач требуется применение специализированной техники, что тоже влияет на финальную цену строительства дома.\n' +
            'Чтобы узнать бюджет, на который вы сможете ориентироваться, обратитесь к нам за составлением сметы. Профессиональный проект гарантирует не только полную финансовую прозрачность, но и качество проведения работ и сохранность материалов.\n'
      },
      options: {
        type: [Object, String],
        default: function () {
          return {
            // Фундамент
            foundation: {
              title: 'Фундамент с ж/б плитой пола',
              value: 0,
              items: [
                { value: 0, text: 'нет' },
                { value: 5400, text: 'Ленточный' },
                { value: 5000, text: 'Свайно-ростверковый' },
                { value: 7000, text: 'Плитный' }
              ]
            },
            // Материал
            material: {
              title: 'Материал несущих стен (без перегородок)',
              value: 0,
              items: [
                { value: 0, text: 'нет' },
                { value: 6000, text: 'Кирпич бутовый, 380мм' },
                { value: 4500, text: 'Газосиликатный блок, 300мм' },
                { value: 5500, text: '«Теплая керамика» (POROMAX), 380мм' },
              ]
            },
            // Межэтажное перекрытие
            interfloorOverlap: {
              title: 'Межэтажное перекрытие',
              value: 0,
              items: [
                { value: 0, text: 'нет' },
                { value: 3500, text: 'Монолитная плита с ж/б лестницей' },
                { value: 2600, text: 'По деревянным балкам с деревянной лестницей' },
              ]
            },
            // Кровля
            roof: {
              title: 'Кровля с чердачным перекрытием',
              value: 0,
              items: [
                { value: 0, text: 'нет' },
                { value: 4000, text: 'Металлочерепица' },
                { value: 5500, text: 'Цементно-песчаная черепица BRAAS' },
                { value: 4100, text: 'Фальцевая кровля' },
                { value: 4500, text: 'Гибкая черепица (SHINGLAS)' },
                { value: 5500, text: 'Плоская ж/б плита с утеплением и ПВХ  мембраной' },
                { value: 7000, text: 'Керамическая черепица BRAAS' },
              ]
            },
            // Отделка фасада
            facadeDecoration: {
              title: 'Отделка фасада',
              value: 0,
              items: [
                { value: 0, text: 'нет' },
                { value: 1500, text: '«Гибкий» клинкер' },
                { value: 2500, text: '«Короед»' },
                { value: 3400, text: 'Керамический облицовочный кирпич' },
              ]
            },
            // Окна
            window: {
              title: 'Окна',
              value: 0,
              items: [
                { value: 0, text: 'нет' },
                { value: 6000, text: 'Металлопластиковые без ламинации (белые)' },
                { value: 7000, text: 'Металлопластиковые с ламинацией (под дерево или цветные)' },
                { value: 11000, text: 'Алюминиевые' },
              ]
            },
          }
        }
      }
    },
    data() {
      return {
        result: null,
        resultArea: null,
        inputData: {
          long: 0,
          width: 0,
          area: '1'
        }
      }
    },
    methods: {
     allCalc() {
       this.result =  this.foundationCalc + this.materialCalc + this.interfloorOverlapCalc + this.roofCalc + this.facadeDecorationCalc + this.windowCalc
       this.resultArea = this.result / this.buildingArea
     },
      clearInput(event) {
       if(event.target.value == 0) {
         event.target.value = ''
       }
      },
      filterKeys(code) {
       const map = {
          'ArrowLeft': true,
          'ArrowRight': true,
          'Backspace': true,
          'Period': true,
          'Comma': true,
          'Digit1': true,
          'Digit2': true,
          'Digit3': true,
          'Digit4': true,
          'Digit5': true,
          'Digit6': true,
          'Digit7': true,
          'Digit8': true,
          'Digit9': true,
          'Digit0': true,
          'Slash': true,
          'Numpad1': true,
          'Numpad2': true,
          'Numpad3': true,
          'Numpad4': true,
          'Numpad5': true,
          'Numpad6': true,
          'Numpad7': true,
          'Numpad8': true,
          'Numpad9': true,
          'Numpad0': true,
          'NumpadDecimal': true
        }
        if(map[code]) {
          return true
        } else {
          return false
        }
      },
      changeDown(event) {
       if(this.filterKeys(event.code)) {
         if(event.code === 'Comma' || event.code === 'Slash') {
           event.preventDefault()
           event.target.value = event.target.value + '.'
         }
       } else {
         event.preventDefault()
       }
      }
    },
    computed: {
      // Этажность
      floors() {
        if (this.inputData.area === '1-M' || this.inputData.area === '2-M' || this.inputData.area === '3-M') {
          return parseFloat(this.inputData.area) + 1
        } else {
          return parseFloat(this.inputData.area)
        }

      },
      // Строительная площадь
      buildingArea() {
        return this.inputData.long * this.inputData.width * this.floors
      },
      // Площадь фасада
      facadeArea() {
        return  ((this.inputData.long * 2) + (this.inputData.width * 2)) * 3 * this.floors
      },
      // Площадь окон
      windowArea() {
        return  this.facadeArea * 0.15
      },
      // Мансардный ли?
      attic() {
        if(this.inputData.area === '1-M' || this.inputData.area === '2-M' || this.inputData.area === '3-M') {
          return true
        }
        return false
      },

      // Вычисления услуг!
      foundationCalc() {
        if (this.attic) {
          return (this.buildingArea * this.options.foundation.value /  (this.floors - 1)) * 0.8
        } else if(this.floors === 1) {
          return  (this.buildingArea * this.options.foundation.value / this.floors) * 0.8
        }  else {
          return this.buildingArea * this.options.foundation.value / this.floors
        }

      },
      materialCalc() {
        if (this.attic) {
          return (this.options.material.value * this.buildingArea) * (this.floors - 1) * 0.8
        } else {
          return this.options.material.value * this.buildingArea
        }

      },
      interfloorOverlapCalc() {
        if (this.attic) {
          if(this.floors > 3) {
            return  (this.options.interfloorOverlap.value * this.buildingArea / (this.floors - 1)) * 0.8
          } else {
            return  (this.options.interfloorOverlap.value * this.buildingArea / 2) * 0.8
          }
        } else {
          if(this.floors == 3) {
            return this.options.interfloorOverlap.value * this.buildingArea / this.floors
          } else {
            return this.options.interfloorOverlap.value * this.buildingArea / 2
          }
        }
      },
      roofCalc() {
        if (this.attic) {
          return (this.options.roof.value * this.buildingArea / (this.floors - 1)) * 0.8
        } else {
          return this.options.roof.value * this.buildingArea / this.floors
        }

      },
      facadeDecorationCalc() {
        if (this.attic) {
          return (this.options.facadeDecoration.value * this.facadeArea) * 0.8
        } else {
          return this.options.facadeDecoration.value * this.facadeArea
        }

      },
      windowCalc() {
        if (this.attic) {
          return (this.options.window.value * this.windowArea) * 0.8
        } else {
          return this.options.window.value * this.windowArea
        }
      },
    }
  }
</script>

<style lang="scss">
  .main-calc-wrapper__radio-label-item {
    cursor: pointer;
  }
  a {
    color: inherit;
  }
  a:hover {
    text-decoration: none;
  }
  .custom-control {
    padding-left: 0;
  }
.main-calc-wrapper {
  &__radio-label-list {
    display: flex;
    align-items: center;
    justify-content: space-around;
    flex-wrap: nowrap;
    margin-bottom: 20px;
  }
  &__radio-label-item.active {
    filter: none;
  }
  &__radio-label-item {
    flex: 0 0 calc(100% / 6);
    max-width: calc(100% / 6);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    filter: grayscale(100%);
    text-align: center;

    img {
      width: auto;
    }
    .custom-control-label {
      padding-top: 20px;
      padding-bottom: 20px;
    }
    .custom-control-label::after, .custom-control-label::before {
      top: 100%;
      left: 46%;

    }
    .custom-control-label::before {
      background-color: #fe9c01!important;
      border-color: #fe9c01!important;
    }
  }
  &__computed-value {
    font-weight: 700;
    font-size: 20px;
  }
  &__service-value {
    font-weight: 700;
    font-size: 20px;
    padding-top: 33px;
  }
  &__result-wrapper {
    border: 2px solid #c82333;
    padding: 15px;
    margin-top: 10px;
    margin-bottom: 10px;
  }
  &__result-value {
    font-size: 22px;
    font-weight: 700;
  }
  &__result-area {
    font-size: 22px;
    font-weight: 700;
    margin-bottom: 20px;
  }
}
.calc-step {
  font-weight: 700;
  font-size: 21px;
  color: #c82333;
}
.main-calc-wrapper__radio-label-list {
   margin-bottom: 40px;
 }

@media screen and (max-width: 900px) {
  .main-calc-wrapper__radio-label-list {
    flex-wrap: wrap;
  }
  .main-calc-wrapper__radio-label-item {
    flex: 0 0 calc(100% / 2);
    max-width: calc(100% / 2);
  }
}
</style>
