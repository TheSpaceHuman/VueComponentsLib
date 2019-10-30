<template>
  <div class="container">
    <div class="row">
      <!--Column left-->
      <div class="col-9 col-md-9 p-0 mb-5">
        <small class="calc-step">Шаг 1</small>
        <h4 class="title--4">{{ lorem.group1 }}</h4>
        <div class="calc-row">
          <div class="column-1-3">
            <!--Input 1-->
            <b-form-group
                class="metric--meter"
                label="Длина"
                label-for="NarStenPanelLength"
            >
              <b-form-input
                  id="NarStenPanelLength"
                  type="text"
                  :class="{ 'is-invalid': $v.NarStenPanelLength.$error && errorMessages, 'animated shake': !$v.NarStenPanelLength.required && errorMessages}"
                  v-model.trim.number="$v.NarStenPanelLength.$model"
                  placeholder="Введите длину" />
              <div class="error"  v-if="!$v.NarStenPanelLength.required && errorMessages">
                Обязательное поле
              </div>
              <div class="error"  v-if="!$v.NarStenPanelLength.numeric && errorMessages">
                Поле должно состоять только из цифр
              </div>
            </b-form-group>
          </div>
          <div class="column-2-3">
            <!--Input 2-->
            <b-form-group
                class="metric--meter"
                label="Ширина"
                label-for="NarStenPanelWidth"
            >
              <b-form-input
                  id="NarStenPanelWidth"
                  type="text"
                  :class="{ 'is-invalid': $v.NarStenPanelWidth.$error && errorMessages, 'animated shake': !$v.NarStenPanelWidth.required && errorMessages}"
                  v-model.trim.number="$v.NarStenPanelWidth.$model"
                  placeholder="Введите ширину" />
              <div class="error"  v-if="!$v.NarStenPanelWidth.required && errorMessages">
                Обязательное поле
              </div>
              <div class="error"  v-if="!$v.NarStenPanelWidth.numeric && errorMessages">
                Поле должно состоять только из цифр
              </div>
            </b-form-group>
          </div>
          <div class="column-3-3 decor-grid-wrapper">
            <div class="decor-grid"></div>
          </div>
        </div>
      </div>
      <div class="col-9 col-md-9 p-0 mb-5">
        <small class="calc-step">Шаг 2</small>
        <h4 class="title--4">{{ lorem.group2 }}</h4>
        <div class="calc-row">
          <div class="column-1-2">
            <!--Input 3-->
            <b-form-group
                label="Длина всех перегородок"
                label-for="MegkomPeregLength"
                class="metric--meter input--320"
            >
              <b-form-input
                  id="MegkomPeregLength"
                  type="text"
                  v-model="MegkomPeregLength"
                  placeholder="Введите длину перегородки" />
            </b-form-group>
          </div>
          <div class="column-2-2 decor-grid-wrapper">
            <div class="decor-grid"></div>
          </div>
        </div>
      </div>

      <div class="col-9 col-md-9 p-0 mb-5">
        <small class="calc-step">Шаг 3</small>
        <h4 class="title--4">{{ lorem.group3 }}</h4>
        <div class="calc-row">
          <div class="column-1-3">
            <!--Checkbox-->
            <b-form-checkbox
                id="KrowPanel"
                name="KrowPanel"
                v-model="KrowPanel"
                class="mb-4"

            >
              В наличии!
            </b-form-checkbox>
          </div>
          <div class="column-2-2-3">
            <div v-if="KrowPanel">
              <!--Input 4-->
              <b-form-group
                  class="metric--deg"
                  label="Угол кровли"
                  label-for="KrowPanelDeg"

              >
                <b-form-input
                    style="width: 250px;"
                    id="KrowPanelDeg"
                    type="text"
                    v-model="KrowPanelDeg"
                    :class="{'is-invalid': $v.KrowPanelDeg.$error, 'animated shake': !$v.KrowPanelDeg.between && errorMessages}"
                    placeholder="Введите угол кровли" />
                <div class="error"  v-if="!$v.KrowPanelDeg.between">
                  От {{$v.KrowPanelDeg.$params.between.min}} - {{$v.KrowPanelDeg.$params.between.max}} градусов.
                </div>
              </b-form-group>
            </div>
          </div>

          <div class="d-none">
            <!--Input 5-->
            <b-form-group
                label="Длина ската, м"
                label-for="KrowPanelLength"
            >
              <b-form-input
                  id="KrowPanelLength"
                  type="text"
                  disabled
                  v-model="KrowPanelLength"
                  placeholder="Введите длину ската" />
            </b-form-group>
            <!--Input 6-->
            <b-form-group
                label="Ширина ската, м"
                label-for="KrowPanelWidth"
            >
              <b-form-input
                  id="KrowPanelWidth"
                  type="text"
                  disabled
                  v-model="KrowPanelWidth"
                  placeholder="Введите ширину ската" />
            </b-form-group>
          </div>
        </div>


      </div>
      <div class="col-9 col-md-9 p-0 mb-5">
        <small class="calc-step">Шаг 4</small>
        <h4 class="title--4">Итого</h4>
        <div class="calc-row">
          <div class="column-1-2">
            <button class="btn-default" @click="totalCount">Подсчитать</button>
          </div>
          <div class="column-2-2">
            <div class="total-price">{{ total | currency('', 0, { thousandsSeparator: ' ' }) }} <span>₽</span></div>
          </div>
        </div>
      </div>

      <!--Table-->
      <div class="col-9 col-md-9 p-0 d-none">
        <b-table striped v-if="tableResult" hover :items="tableResult" />
      </div>
    </div>
  </div>
</template>

<script>
  import '../plugins/mathRound'
  import { required, between, numeric } from 'vuelidate/lib/validators'

  export default {
    name: "Calc13",
    data() {
      return {
        lorem: {
          name: 'Изовер Друхэтажный (пол ППС)',
          leftColumnTitle: 'Входные данные',
          rightColumnTitle: 'Результат',
          group1: 'Наружные стеновые панели',
          group2: 'Межкомнатные перегородки',
          group3: 'Кровельные панели'
        },
        NarStenPanelLength: null,
        NarStenPanelWidth: null,
        MegkomPeregLength: null,
        KrowPanel: false,
        KrowPanelDeg: 0,
        KrowPanelLength: null,
        KrowPanelWidth: null,

        total: 0,
        isValid: false,
        errorMessages: null,
        //Количество бруса
        KolBrusaNapPanel: 0, //На напольные панели
        KolBrusaNarPanel: 0, //На наружные стеновые панели
        KolBrusaMegkPanel: 0, //На межкомнатные перегородки 38*89
        KolBrusaKrowPanel: 0, //На кровельные панели 46*146

        objCost: {
          //Напольные панели
          NapPanel: {},
          //Наружные стеновые панели
          NarPanel: {},
          //Межкомнатные перегородки
          MegkPereg: {},
          //Кровельные панели
          KrowPanel: {}
        },
        brusPrice: [168, 168, 105, 168],
        //Расходные материалы
        сonsumablesPrice: [300, 1.10, 3.20, 20, 1500],
        objConsumables: {},
        mezhetPok: null,
        showTable: false,
        tableResult: []
      }
    },
    methods: {
      validation() {
        this.$v.$touch()
        if (this.$v.$invalid) {
          this.errorMessages = true
          return
        } else {
          this.errorMessages = false
        }
      },
      totalCount() {
        this.validation()
        if (!this.errorMessages) {
          const result = this.CountNapolPanel(5180) +
            this.CountNarStenPanel(2300) +
            this.CostMegkomPereg(3850) +
            this.CostKrowPanel(1920) +
            this.CountBrus(this.objCost, this.brusPrice) +
            this.CountConsumables(this.objCost, this.сonsumablesPrice) +
            this.RaskAndBrus() +
            this.mezhetPok

          this.total = Math.round10(result, -1)
          this.showTable = true
        }

      },
      //Напольные панели
      CountNapolPanel(costPanel) {
        const length = this.NarStenPanelLength
        const width = this.NarStenPanelWidth

        let countPanelLength = Math.ceil(length / 1.2)
        let countPanelWidth = Math.ceil(width / 2.7)
        const allPanel = countPanelLength * countPanelWidth

        this.objCost.NapPanel = {allPan: allPanel}

        const result = allPanel * costPanel

        //Добавления элементов в результирующую таблицу
        let tableResult = this.tableResult
        let flag = true
        tableResult.forEach(function(item) {
          if (item['title'] === 'Напольные панели') {
            flag = false
          }
        });
        if(flag) {
          this.tableResult.push({title: 'Напольные панели', value: result })
        } else {
          tableResult.forEach(function(item) {
            if (item['title'] === 'Напольные панели') {
              item['value'] = result
            }
          });
        }


        return result
      },
      //Наружные стеновые панели
      CountNarStenPanel(costPanel) {
        const COST_PANEL = costPanel

        let countPanelLength = Math.ceil((this.NarStenPanelLength - 0.156) / 0.6 * 2) + Math.ceil((this.NarStenPanelLength - 0.156) / 0.6)
        let countPanelWidth = Math.ceil((this.NarStenPanelWidth - 0.156) / 0.6 * 2) + Math.ceil((this.NarStenPanelWidth - 0.156) / 0.6)
        let allPanel = countPanelLength + countPanelWidth

        this.objCost.NarPanel = {allPan: allPanel}

        const result = allPanel * COST_PANEL

        //Добавления элементов в результирующую таблицу
        let tableResult = this.tableResult
        let flag = true
        tableResult.forEach(function(item) {
          if (item['title'] === 'Наружные стеновые панели') {
            flag = false
          }
        });
        if(flag) {
          this.tableResult.push({title: 'Наружные стеновые панели', value: result })
        } else {
          tableResult.forEach(function(item) {
            if (item['title'] === 'Наружные стеновые панели') {
              item['value'] = result
            }
          });
        }

        return result
      },
      //Межкомнатные перегородки
      CostMegkomPereg(costPanel) {
        const COST_PANEL = costPanel
        if (this.MegkomPeregLength == null || this.MegkomPeregLength == '') {
          this.MegkomPeregLength = 0
        }

        let countPeregLength = Math.ceil(this.MegkomPeregLength / 1.2)
        let allPanel = countPeregLength

        this.objCost.MegkPereg = {allPan: allPanel}

        const result = allPanel * COST_PANEL

        //Добавления элементов в результирующую таблицу
        let tableResult = this.tableResult
        let flag = true
        tableResult.forEach(function(item) {
          if (item['title'] === 'Межкомнатные перегородки') {
            flag = false
          }
        });
        if(flag) {
          this.tableResult.push({title: 'Межкомнатные перегородки', value: result })
        } else {
          tableResult.forEach(function(item) {
            if (item['title'] === 'Межкомнатные перегородки') {
              item['value'] = result
            }
          });
        }

        return result
      },
      //Кровельные панели
      CostKrowPanel(costPanel) {
        if (this.KrowPanel) {
          const x = (this.NarStenPanelWidth / 2) / Math.cos(this.degToRad(this.KrowPanelDeg)) + 0.3
          this.KrowPanelLength = Math.round10(x, -1)
          const y = parseInt(this.NarStenPanelLength) + 0.6
          this.KrowPanelWidth = Math.round10(y, -1)
          let countPanelLength = Math.ceil(this.KrowPanelLength * 2 / 2.5)
          let countPanelWidth = Math.ceil(y / 0.625)
          let allPanel = countPanelLength * countPanelWidth

          this.objCost.KrowPanel = {
            widthPan: countPanelWidth,
            length: this.KrowPanelLength,
            width: this.KrowPanelWidth,
            allPan: allPanel
          }

          const result = allPanel * costPanel

          //Добавления элементов в результирующую таблицу
          let tableResult = this.tableResult
          let flag = true
          tableResult.forEach(function(item) {
            if (item['title'] === 'Кровельные панели') {
              flag = false
            }
          });
          if(flag) {
            this.tableResult.push({title: 'Кровельные панели', value: result })
          } else {
            tableResult.forEach(function(item) {
              if (item['title'] === 'Кровельные панели') {
                item['value'] = result
              }
            });
          }

          return result

        } else {
          this.KrowPanelLength = 0
          this.KrowPanelWidth = 0
          this.objCost.KrowPanel = {
            widthPan: 0,
            length: 0,
            width: 0,
            allPan: 0
          }
          return 0
        }
      },

      //Количество бруса
      CountBrus(obj, price) {

        let NapPanel = obj.NapPanel
        let NarPanel = obj.NarPanel
        let MegkPereg = obj.MegkPereg
        let KrowPanel = obj.KrowPanel
        //Количество, шт (по 6м)
        const CountNapPanelCol1 = Math.ceil(NapPanel.allPan * 10.5 / 6)
        const CountNarPanelCol1 = Math.ceil(NarPanel.allPan * 5.4 / 6 * 1.2)
        const CountMegkPeregCol1 = Math.ceil(MegkPereg.allPan * 6 * 1.2 / 6)
        const CountKrowPanelCol1 = Math.ceil(((Math.ceil(KrowPanel.length / 2.5) * 2 * KrowPanel.width + 2 * KrowPanel.width * 1.05) / 6)) +
          Math.ceil((((KrowPanel.widthPan + 1) * (KrowPanel.length * 2) * 1.05) / 6))
        //Количество, м.п
        const CountNapPanelCol2 = CountNapPanelCol1 * 6
        const CountNarPanelCol2 = CountNarPanelCol1 * 6
        const CountNapPanelCol2_CountNarPanelCol2 = CountNapPanelCol2 + CountNarPanelCol2
        const CountMegkPeregCol2 = CountMegkPeregCol1 * 6
        const CountKrowPanelCol2 = CountKrowPanelCol1 * 6
        const CountMegkPeregCol2_CountKrowPanelCol2 = CountMegkPeregCol2 + CountKrowPanelCol2
        //Стоимость
        const NapPanelTotal = CountNapPanelCol2 * price[0]
        const NarPanelTotal = CountNarPanelCol2 * price[1]
        const MegkPeregTotal = CountMegkPeregCol2 * price[2]
        const KrowPanelTotal = CountKrowPanelCol2 * price[3]
        //Итог
        const TotalCost = NapPanelTotal + NarPanelTotal + MegkPeregTotal + KrowPanelTotal


        //Добавления элементов в результирующую таблицу
        let tableResult = this.tableResult
        let flag = true
        tableResult.forEach(function(item) {
          if (item['title'] === 'Количество бруса') {
            flag = false
          }
        });
        if(flag) {
          this.tableResult.push({title: 'Количество бруса', value: TotalCost })
        } else {
          tableResult.forEach(function(item) {
            if (item['title'] === 'Количество бруса') {
              item['value'] = TotalCost
            }
          });
        }

        return TotalCost

      },
      //Расходные материалы
      CountConsumables(obj, price) {
        const totalAllPanel = obj.NapPanel.allPan + obj.NarPanel.allPan + obj.MegkPereg.allPan + obj.KrowPanel.allPan
        //Пена монтажная
        const montPena = Math.ceil(totalAllPanel / 1.5)
        //Саморезы 3,8*45
        const smorez45 = Math.ceil(totalAllPanel * 150)
        //Шуруп 7,5*112
        let shurupInt = parseInt(this.NarStenPanelLength * 4) + parseInt(this.NarStenPanelWidth * 4) + parseInt(this.MegkomPeregLength)
        const shurup = Math.ceil(shurupInt)
        //Саморезы 4,2*90
        const smorez90 = shurup * 4

        const CostMontPena = montPena * price[0]
        const CostSmorez45 = smorez45 * price[1]
        const CostSmorez90 = smorez90 * price[2]
        const CostShurup = shurup * price[3]


        //Сумма
        const result = CostMontPena + CostSmorez45 + CostSmorez90 + CostShurup

        //Межэтажное перекрытие
        const mezhetPok = this.NarStenPanelLength * this.NarStenPanelWidth
        const CostmezhetPok = mezhetPok * price[4]
        this.mezhetPok = CostmezhetPok


        //Добавления элементов в результирующую таблицу
        let tableResult = this.tableResult
        let flag = true
        tableResult.forEach(function(item) {
          if (item['title'] === 'Расходные материалы') {
            flag = false
          }
        });
        if(flag) {
          this.tableResult.push({title: 'Расходные материалы', value: result })
        } else {
          tableResult.forEach(function(item) {
            if (item['title'] === 'Расходные материалы') {
              item['value'] = result
            }
          });
        }

        //Добавления элементов в результирующую таблицу
        let tableResult2 = this.tableResult
        let flag2 = true
        tableResult2.forEach(function(item) {
          if (item['title'] === 'Межэтажное перекрытие') {
            flag2 = false
          }
        });
        if(flag2) {
          this.tableResult.push({title: 'Межэтажное перекрытие', value: CostmezhetPok })
        } else {
          tableResult.forEach(function(item) {
            if (item['title'] === 'Межэтажное перекрытие') {
              item['value'] = CostmezhetPok
            }
          });
        }


        return result
      },
      //Раскрой и обрусовка согласно карты раскроя
      RaskAndBrus() {
        const result = (this.CountNapolPanel(5180) +
          this.CountNarStenPanel(2300) +
          this.CostMegkomPereg(3850) +
          this.CostKrowPanel(1920) +
          this.CountBrus(this.objCost, this.brusPrice) +
          this.CountConsumables(this.objCost, this.сonsumablesPrice)) * 0.15

        //Добавления элементов в результирующую таблицу
        let tableResult = this.tableResult
        let flag = true
        tableResult.forEach(function(item) {
          if (item['title'] === 'Раскрой и обрусовка согласно карты раскроя') {
            flag = false
          }
        });
        if(flag) {
          this.tableResult.push({title: 'Раскрой и обрусовка согласно карты раскроя', value: Math.round10(result, -1) })
        } else {
          tableResult.forEach(function(item) {
            if (item['title'] === 'Раскрой и обрусовка согласно карты раскроя') {
              item['value'] = Math.round10(result, -1)
            }
          });
        }

        return result
      },
      //Преобразование градусов в радианы
      degToRad(deg) {
        return deg / 180 * Math.PI;
      },
      //Преобразование радиан в градусы
      radToDeg(rad) {
        return rad / Math.PI * 180;
      }

    },
    validations: {
      KrowPanelDeg: {
        between: between(0, 360)
      },
      NarStenPanelLength: {
        required,
        numeric
      },
      NarStenPanelWidth: {
        required,
        numeric
      }
    },
    props: ['name']
  }
</script>

<style lang="scss">

</style>
