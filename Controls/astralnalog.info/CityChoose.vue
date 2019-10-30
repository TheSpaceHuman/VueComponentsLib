<template>
  <div class="city-choose-wrapper">
    <button type="button" class="btn_city" @click="$refs.modal.open()">{{ compCity }}</button>
    <SweetModal ref="modal"  title="Выберите свой город">
      <div class="city-choose-wrapper_modal">
        <el-row type="flex" style="margin-bottom: 20px;">
          <el-col :span="24">
            <el-select
                v-model="value"
                filterable
                remote
                reserve-keyword
                placeholder="Выберите город"
                :remote-method="remoteMethod"
                :loading="loading"
                @change="selectedCity"
            >
              <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.label"
              ></el-option>
            </el-select>
          </el-col>
        </el-row>
        <el-row type="flex" style="margin-bottom: 20px;">
          <el-col :span="8">
            <ul class="city-choose_city-list">
              <li class="city-choose_city-item" v-for="item in cityArr1">
                <button class="btn_link" type="button" @click="selectedCityLink(item)"><b>{{item}}</b></button>
              </li>
            </ul>
          </el-col>
          <el-col :span="8">
            <ul class="city-choose_city-list">
              <li class="city-choose_city-item" v-for="item in cityArr2">
                <button class="btn_link" type="button" @click="selectedCityLink(item)">{{item}}</button>
              </li>
            </ul>
          </el-col>
          <el-col :span="8">
            <ul class="city-choose_city-list">
              <li class="city-choose_city-item" v-for="item in cityArr3">
                <button class="btn_link" type="button" @click="selectedCityLink(item)">{{item}}</button>
              </li>
            </ul>
          </el-col>
        </el-row>

      </div>
    </SweetModal>
  </div>
</template>

<script>
  import axios from 'axios'
  import Cookies from 'js-cookie'

  export default {
    props: {
      cityArr1: {
        type: [ String, Array ],
        default: function () {
          return ['Москва', 'Санкт-Петербург', 'Калуга', 'Новосибирск', 'Омск', 'Воронеж', 'Саратов', 'Томск']
        }
      },
      cityArr2: {
        type: [ String, Array ],
        default: function () {
          return ['Белгород','Благовещенск', 'Владимир', 'Волгоград', 'Екатеринбург', 'Иркутск', 'Калининград', 'Липецк', 'Новый Уренгой']
        }
      },
      cityArr3: {
        type: [ String, Array ],
        default: function () {
          return ['Пермь','Самара', 'Симферополь', 'Смоленск', 'Сургут', 'Тамбов', 'Тверь', 'Тюмень']
        }
      },
      city: {
        type: String,
        default: 'Москва'
      }
    },
    data () {
      return {
        options: [],
        value: [],
        loading: false,

      }
    },
    methods: {
      remoteMethod(query) {
        if (query !== '') {
          this.loading = true;
          axios.get(`https://cors-anywhere.herokuapp.com/http://kladr-api.ru/api.php`, {
                params: {
                  query: query,
                  contentType: 'city',
                  limit: 10
                }
              })
              .then(res => {
                res.data.result.map(item => {
                  if(this.options.find(el => el.value === item.id) === undefined) {
                    this.options.push({ value: item.id, label: item.name })
                  }
                })
              })

              .catch(e => console.log(e))
              this.loading = false;
        } else {
          this.options = []
        }
      },
      selectedCity() {
        this.city = this.value
        Cookies.remove('currentCity');
        Cookies.set('currentCity', this.value)
        this.$refs.modal.close()
        document.location.reload()
      },
      selectedCityLink(item) {
        this.city = item
        Cookies.remove('currentCity');
        Cookies.set('currentCity', item)
        this.$refs.modal.close()
        document.location.reload()
      },
    },
    computed: {
      compCity() {
        if (Cookies.get('currentCity') !== undefined) {
          return   Cookies.get('currentCity')
        }
        return this.city
      }
    }
  }
</script>

<style lang="scss">
@import "~element-ui/lib/theme-chalk/option.css";
@import "~element-ui/lib/theme-chalk/select.css";
@import "~element-ui/lib/theme-chalk/row.css";
@import "~element-ui/lib/theme-chalk/col.css";

.city-choose-wrapper {
  margin: 50px;
  position: relative;
  font: inherit;
  &_modal {
    position: relative;
  }
}
.el-select-dropdown.el-popper {
  z-index: 200000!important;
}
.btn_city {
  background: transparent;
  padding: 0;
  font-size: 16px;
  font-weight: 400;
  color: #000;
  border: 0;
}
.btn_link {
  background: transparent;
  padding: 0;
  border: 0;
  border-bottom: 1px dashed #000;
  font-weight: 500;
  font-family: inherit;
  font-size: 16px;
}
.city-choose_city-list {
  margin: 0;
  padding: 0;
  list-style: none;
}
.city-choose_city-item {
  padding: 4px 5px;
}
.el-select {
  width: 100%;
}
</style>
