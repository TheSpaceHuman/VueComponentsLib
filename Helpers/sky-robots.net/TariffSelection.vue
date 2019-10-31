<template>
  <div class="tariff-selection">
    <div class="tariff-selection__items row justify-content-around">
      <div class="col-12 col-md-6" v-if="type === 'continue'">
        <div class="tariff-selection__item card">
          <h4 class="tariff-selection__item__title text-center h3">{{ currentPackage.title }}</h4>
          <div class="tariff-selection__item__price text-center py-4">
            <span>{{ currentPackage.price_month }} / месяц</span>
            <br>
            <span>{{ currentPackage.price_year }} / год</span>
          </div>
          <div class="tariff-selection__item__actions">
            <button
              @click="updateTariff(currentPackage.id, 30)"
              type="button"
              class="btn btn-success m-2">Продлить на месяц</button>
            <button
              @click="updateTariff(currentPackage.id, 365)"
              type="button"
              class="btn btn-danger m-2">Продлить на год</button>
          </div>
        </div>
      </div>
      <div
        v-else-if="type === 'change'"
        v-for="pack in packagesParse"
        :key="pack.id"
        class="col-12 col-md-4 col-lg-3"
      >
        <div
          :class="{'active': pack.id == user.package_id}"
          class="tariff-selection__item card"
        >
          <h4 class="tariff-selection__item__title text-center h3">{{ pack.title }}</h4>
          <div class="tariff-selection__item__price text-center py-4">
            <span>{{ pack.price_month }} / месяц</span>
            <br>
            <span>{{ pack.price_year }} / год</span>
          </div>
          <div class="tariff-selection__item__actions">
            <button
              @click="updateTariff(pack.id, 30)"
              type="button"
              class="btn btn-success m-2">Купить на месяц</button>
            <button
              @click="updateTariff(pack.id, 365)"
              type="button"
              class="btn btn-danger m-2">Купить на год</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import toastr from 'toastr'
  import axios from  'axios'
  import $ from 'jquery'
  export default {
    name: 'TariffSelection',
    props: {
      packages: {
        // JSON
        type: String,
        required: true,
      },
      action: {
        required: true
      },
      type: {
        // continue | change
        type: String,
        default: 'change'
      },
      user: {
        // JSON
        type: String,
        required: true,
      }

    },
    data() {
      return {}
    },
    methods: {
      hideModal() {
        $('.modal').modal('hide')
      },
      async updateTariff(id, days) {
        try {
          const res = await axios({
            method: 'post',
            url: this.action,
            data: {
              days: days,
              userId: this.userParse.id,
              packageId: id
            }
          });
          if(res.data.message.type === 'success') {
            toastr.success(res.data.message.body);
            setTimeout(this.hideModal, 500)
          } else {
            toastr.error('Что-то пошло не так');
          }
        } catch (e) {
          console.log(e)
        }
      }
    },
    computed: {
      packagesParse() {
        return JSON.parse(this.packages)
      },
      userParse() {
        return JSON.parse(this.user)
      },
      currentPackage() {
        const index = this.packagesParse.findIndex((el) => el.id == this.userParse.package_id)
        if(index !== -1) {
          return this.packagesParse[index]
        }
        return false
      }
    }
  }
</script>

<style lang="scss">
  @import "../../../sass/variables";

  .tariff-selection {

    &__item {
      padding: 12px;
      &__actions {
        display: flex;
        justify-content: space-around;
        flex-wrap: wrap;

        button, a {
          white-space: nowrap;
          font-size: 11px;
        }
      }
    }
    &__item.active {
      border-color: $green;
    }
  }
</style>