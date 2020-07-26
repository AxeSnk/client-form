<template>
  <div class="register">
    <h1>Новый клиент</h1>
    <hr>

    <form class="register__form" @submit.prevent="submitHandler">

      <div class="attributes">

        <div class="input-field">
          <label class="input-label required-label">Фамилия</label>
          <input 
            type="text" 
            id="lastname" 
            v-model.trim="lastname" 
            :class="{invalid: ($v.lastname.$dirty && !$v.lastname.required)}">
          <small
            class="helper-text invalid"
            v-if="$v.lastname.$dirty && !$v.lastname.required"
          >обязательно для заполнения</small>
        </div>
      
        <div class="input-field">
          <label class="input-label required-label">Имя</label>
          <input 
            type="text" 
            id="firstname" 
            v-model.trim="firstname" 
            :class="{invalid: ($v.firstname.$dirty && !$v.firstname.required)}">
          <small
            class="helper-text invalid"
            v-if="$v.firstname.$dirty && !$v.firstname.required"
          >обязательно для заполнения</small>
        </div>

        <div class="input-field">
          <label class="input-label">Отчество</label>
          <input 
            type="text" 
            id="middlename">
        </div>

        <div class="input-field">
          <label class="input-label required-label">Дата рождения</label>
          <input 
            type="text" 
            id="birthday" 
            v-model="birthday" 
            :class="{invalid: ($v.birthday.$dirty && !$v.birthday.required) || ($v.birthday.$dirty && $v.birthday.$validDate)}">
          <small
            class="helper-text invalid"
            v-if="$v.birthday.$dirty && !$v.birthday.required"
          >обязательно для заполнения</small>
          <small
            class="helper-text invalid"
            v-else-if="$v.birthday.$dirty && $v.birthday.$validDate"
          >дата в формате ДД.ММ.ГГГГ</small>
        </div>

        <div class="input-field">
          <label class="input-label">Номер телефона</label>
          <input 
            type="number" 
            id="phone"
            v-model="phone" 
            :class="{invalid: ($v.phone.$dirty && !$v.phone.validPhone)}">
          <small
            class="helper-text invalid"
            v-if="$v.phone.$dirty && !$v.phone.validPhone"
          >неверный формат</small>
        </div>

        <div class="input-field">
          <label class="input-label">Пол</label>
          <div class="radio-buttons">
            <label class="radio-buttons__label">мужчина
              <input type="radio" name="sex" checked="checked">
            </label>
            <label class="radio-buttons__label">женщина
              <input type="radio" name="sex">
            </label>
          </div>
        </div>

        <div class="input-field">
          <label class="input-label required-label">Группа клиентов</label>
          <select name="group[]" v-model="group" :class="{invalid: ($v.group.$dirty && !$v.group.required)}">
            <option value="VIP">VIP</option>
            <option value="Проблемные">Проблемные</option>
            <option value="ОМС">ОМС</option>
          </select>
          <small
            class="helper-text invalid"
            v-if="$v.group.$dirty && !$v.group.required"
          >обязательно для заполнения</small>
        </div>

        <div class="input-field">
          <label class="input-label">Лечащий врач</label>
          <select name="doctor[]" v-model="doctor">
            <option value="Иванов">Иванов</option>
            <option value="Захаров">Захаров</option>
            <option value="Чернышева">Чернышева</option>
          </select>
        </div>

        <div class="input-field">
          <label class="input-label">Не отправлять СМС</label>
            <input type="checkbox" v-model="sms">
        </div>


      </div>

      <h2>Адрес</h2>

      <div class="input-field">
        <label class="input-label">Индекс</label>
        <input type="text" id="index">
      </div>

      <div class="input-field">
        <label class="input-label">Страна</label>
        <input type="text" id="country">
      </div>

      <div class="input-field">
        <label class="input-label">Область</label>
        <input type="text" id="area">
      </div>

      <div class="input-field">
        <label class="input-label required-label">Город</label>
        <input type="text" id="city"           
          v-model.trim="city" 
          :class="{invalid: ($v.city.$dirty && !$v.city.required)}">
        <small
          class="helper-text invalid"
          v-if="$v.city.$dirty && !$v.city.required"
        >обязательно для заполнения</small>
      </div>

      <div class="input-field">
        <label class="input-label">Улица</label>
        <input type="text" id="street">
      </div>

      <div class="input-field">
        <label class="input-label">Дом</label>
        <input type="text" id="house">
      </div>

      <h2>Паспорт</h2>

      <div class="input-field">
        <label class="input-label required-label">Тип документа</label>
        <select name="documents[]" v-model="documents" :class="{invalid: ($v.group.$dirty && !$v.group.required)}">
          <option value="Паспорт">Паспорт</option>
          <option value="Свидетельство о рождении">Свидетельство о рождении</option>
          <option value="Вод. удостоверение">Вод. удостоверение</option>
        </select>
        <small
          class="helper-text invalid"
          v-if="$v.documents.$dirty && !$v.documents.required"
        >обязательно для заполнения</small>
      </div>

      <div class="input-field">
        <label class="input-label">Серия</label>
        <input type="number" id="series">
      </div>

      <div class="input-field">
        <label class="input-label">Номер</label>
        <input type="number" id="number">
      </div>

      <div class="input-field">
        <label class="input-label required-label">Дата выдачи</label>
        <input 
          type="text" 
          id="dateOfIssue" 
          v-model="dateOfIssue" 
          :class="{invalid: ($v.dateOfIssue.$dirty && !$v.dateOfIssue.required) || ($v.dateOfIssue.$dirty && $v.dateOfIssue.$validDate)}">
        <small
          class="helper-text invalid"
          v-if="$v.dateOfIssue.$dirty && !$v.dateOfIssue.required"
        >обязательно для заполнения</small>
        <small
          class="helper-text invalid"
          v-else-if="$v.dateOfIssue.$dirty && $v.dateOfIssue.$validDate"
        >дата в формате ДД.ММ.ГГГГ</small>
      </div>

      <div class="button__wrapper">
        <button class="button">Создать</button>
      </div>

    </form>
  </div>
</template>

<script>
import {required, minLength} from 'vuelidate/lib/validators';
import {valdate, floatRegExp} from './validHelpers'

export default {
  name: 'register',
  data: () => ({
    lastname: '',
    firstname: '',
    birthday: '',
    phone: '',
    group: '',
    doctor: '',
    sms: '',
    city: '',
    documents: '',
    dateOfIssue: ''
  }),
  validations: {
    lastname: {required},
    firstname: {required},
    birthday: {
      required,
      validDate: val => {
        valdate.lastIndex = 0
        return valdate.test(val)
      }
    },
    phone: {
      validPhone: val => {
        floatRegExp.lastIndex = 0
        return floatRegExp.test(val)
      }
    },
    group: {required},
    city: {required},
    documents: {required},
    dateOfIssue: {
      required,
      validDate: val => {
        valdate.lastIndex = 0
        return valdate.test(val)
      }

    }
  },
  methods: {
    submitHandler() {
      if (this.$v.$invalid) {
        this.$v.$touch()
        return
      }
      alert("Новый клиент успешно создан!")
    }
  }
}
</script>

<style lang="scss" scoped>
.register__form {
  margin: 0 auto;
  max-width: 600px;
}
.input-field {
  display: flex;
  margin-bottom: 5px;
}
.input-label {
  min-width: 200px;
  position: relative;
  text-align: left;
}
input {
  padding: 2px;
  border: 1px solid #2c3e50;
  border-radius: 2px;
}
input.invalid {
  border: 1px solid #f44336;
}
.helper-text.invalid {
  color: #f44336;
  margin-left: 10px;
}
.required-label::after {
  content: '\2732';
  top: -4px;
  font-size: 10px;
  position: absolute;
}
</style>