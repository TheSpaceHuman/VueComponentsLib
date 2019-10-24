<template>
  <form id="index-form" @submit.prevent="submitForm()">
    <!--is-valid is-invalid-->
    <div class="form-group">
      <label for="name">Имя:</label>
      <input
        id="name"
        type="text"
        class="form-control"
        name="name"
        v-model.trim="form.name"
        :class="{
          'is-invalid': $v.form.name.$invalid && $v.form.name.$dirty,
           'is-valid': !$v.form.name.$invalid && $v.form.name.$dirty
         }"
        @blur="$v.form.name.$touch()"
        placeholder="Иван">
      <div class="invalid-feedback" v-if="!$v.form.name.required && $v.form.name.$dirty">Поле обязательное</div>
    </div>
    <div class="form-group">
      <label for="email">E-mail:</label>
      <input
        id="email"
        type="text"
        class="form-control"
        name="email"
        v-model.trim="form.email"
        placeholder="example@gmail.com"
        :class="{
         'is-invalid': $v.form.email.$invalid && $v.form.email.$dirty,
         'is-valid': !$v.form.email.$invalid && $v.form.email.$dirty
         }"
        @blur="$v.form.email.$touch()"
      >
      <div class="invalid-feedback" v-if="!$v.form.email.required && $v.form.email.$dirty">Поле обязательное</div>
      <div class="invalid-feedback" v-if="!$v.form.email.email && $v.form.email.$dirty">Не валидный email</div>
    </div>
    <div class="form-group">
      <label for="telegram">Ник в Telegram:</label>
      <input id="telegram"
             type="text"
             class="form-control"
             name="telegram"
             v-model.trim="form.telegram"
             placeholder="@Ivan">
    </div>
    <div class="d-flex justify-content-center align-items-center">
      <button
        class="btn btn-danger"
        type="submit"
        :disabled="$v.$invalid"
      >
        Отправить</button>
    </div>
  </form>
</template>

<script>
import axios from  'axios'
import toastr from 'toastr'
import { required, email } from 'vuelidate/lib/validators'
export default {
  name: 'IndexForm',
  props: ['action', 'method'],
  data() {
    return {
      form: {
        name: '',
        email: '',
        telegram: ''
      }
    }
  },
  methods: {
    clearForm() {
      this.form.name = ''
      this.form.email = ''
      this.form.telegram = ''
      this.$v.$reset()
    },
    async submitForm() {
      if(this.$v.$invalid) {
        toastr.error('В форме содержаться ошибки', 'Ошибка');
      } else {
        try {
          console.log('action: ', this.action)
          console.log('form: ', this.form)
          const res = await axios.post(this.action, this.form);
          toastr.success(`Спасибо ${this.form.name}, ваше сообщение успешно отправлено`, 'Успех');
          console.log(res)
          this.clearForm()
        } catch (e) {
          toastr.error('Что-то пошло не так', 'Ошибка');
          console.log(e)
        }
      }

    }
  },
  validations: {
    form: {
      name: {
        required
      },
      email: {
        required, email
      }
    }

  }

}
</script>
