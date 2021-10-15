<template>
  <form class="form" @submit.prevent="onSubmit" autocomplete="off">
    <div class="form__group">
      <label for="name" class="form__label">Имя</label>
      <input
        id="name"
        name="name"
        type="text"
        class="form__input"
        placeholder="Введите Ваше имя"
        v-model.trim="fields.name"
        @blur="checkName"
      />
      <span class="form__error" v-if="errors.errorName">{{ errors.errorName }}</span>
    </div>

    <div class="form__group">
      <label for="email" class="form__label">Email</label>
      <input
        id="email"
        name="email"
        type="email"
        class="form__input"
        placeholder="Введите ваш email"
        v-model.trim="fields.email"
        @blur="checkEmail"
      />
      <span class="form__error" v-if="errors.errorEmail">{{ errors.errorEmail }}</span>
    </div>

    <div class="form__group">
      <label for="tel" class="form__label">Номер телефона</label>
      <input
        id="tel"
        name="tel"
        type="tel"
        class="form__input"
        placeholder="Введите ваш номер телефона"
        v-model.trim="fields.phone"
        @blur="checkPhone"
      />
      <span class="form__error" v-if="errors.errorPhone">{{ errors.errorPhone }}</span>
    </div>

    <div class="form__group">
      <label for="select" class="form__label">Язык</label>
      <app-select
        id="select"
        :options="langOptions"
        @select="optionSelected"
        :selected="fields.selectedLang.name"
        :default="'Язык'"
      ></app-select>
    </div>

    <div class="form__group form__conditions">
      <input type="checkbox" id="conditions" class="form__checkbox" v-model="fields.conditionsAccepted">
      <label for="conditions" class="form__checkbox-label">Принимаю <a href="#">условия</a> использования</label>
    </div>

    <button type="submit" class="form__btn" :disabled="!isFormEnable">Зарегистрироваться</button>
  </form>
</template>

<script>
import AppSelect from './AppSelect'

const regexName = /^[-\sa-zA-Zа-яА-ЯЁё]+$/
const regexEmail = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
const regexPhone = /^(\s*)?(\+)?([-()]?\d[-()]?){11}(\s*)+$/

export default {
  components: {
    AppSelect
  },
  data () {
    return {
      fields: {
        name: '',
        email: '',
        phone: '',
        selectedLang: '',
        conditionsAccepted: false
      },
      errors: {
        errorName: '',
        errorEmail: '',
        errorPhone: ''
      },
      langOptions: [
        {
          name: 'Русский',
          value: 'ru'
        },
        {
          name: 'Английский',
          value: 'en'
        },
        {
          name: 'Китайский',
          value: 'zh'
        },
        {
          name: 'Испанский',
          value: 'es'
        }
      ]
    }
  },
  methods: {
    optionSelected (option) {
      this.fields.selectedLang = option
    },
    validValue (value, regex) {
      return regex.test(value)
    },
    checkName () {
      this.errors.errorName = ''
      if (!this.fields.name) {
        this.errors.errorName = 'Укажите имя'
      } else if (!this.validValue(this.fields.name, regexName)) {
        this.errors.errorName = 'Имя не может содержать цифры и символы кроме пробела и дефиса'
      }
    },
    checkEmail () {
      this.errors.errorEmail = ''
      if (!this.fields.email) {
        this.errors.errorEmail = 'Укажите email'
      } else if (!this.validValue(this.fields.email, regexEmail)) {
        this.errors.errorEmail = 'Введено некорректное значение'
      }
    },
    checkPhone () {
      this.errors.errorPhone = ''
      if (!this.fields.phone) {
        this.errors.errorPhone = 'Укажите номер телефона'
      } else if (!this.validValue(this.fields.phone, regexPhone)) {
        this.errors.errorPhone = 'Введено некорректное значение'
      }
    },
    onSubmit () {
      alert('Успешно!')
    }
  },
  computed: {
    isFormEnable () {
      return Object.values(this.errors).every(x => !x) && Object.values(this.fields).every(x => x)
    }
  }
}
</script>
