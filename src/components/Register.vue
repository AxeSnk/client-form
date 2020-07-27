<template>
  <div class="register">
    <Popup 
      v-if="isPopupVisible"
      @closePopup="closePopup"  
    />
    <h1>Новый клиент</h1>
    <hr>

    <form class="register__form" @submit.prevent="submitHandler">

      <div class="register__form-wrapper">

        <div class="attributes">

          <div 
            class="input-field" 
            :class="{invalid: ($v.lastname.$dirty && !$v.lastname.required)}"
            >
            <label class="input-label required-label">Фамилия</label>
            <input 
              type="text"
              name="lastname" 
              v-model.trim="lastname" 
            >
            <small
              class="helper-text invalid"
              v-if="$v.lastname.$dirty && !$v.lastname.required"
            >обязательно для заполнения</small>
          </div>
        
          <div 
            class="input-field"
            :class="{invalid: ($v.firstname.$dirty && !$v.firstname.required)}"
            >
            <label class="input-label required-label">Имя</label>
            <input 
              type="text"
              name="firstname" 
              v-model.trim="firstname" 
            >
            <small
              class="helper-text invalid"
              v-if="$v.firstname.$dirty && !$v.firstname.required"
            >обязательно для заполнения</small>
          </div>

          <div class="input-field">
            <label class="input-label">Отчество</label>
            <input 
              type="text"
              name="middlename" 
            >
          </div>

          <div 
            class="input-field"
            :class="{invalid: ($v.birthday.$dirty && !$v.birthday.required) || ($v.birthday.$dirty && $v.birthday.$validDate)}"
          >
            <label class="input-label required-label">Дата рождения</label>
            <input 
              type="text"
              name="birthday" 
              v-model="birthday" 
            >
            <small
              class="helper-text invalid"
              v-if="$v.birthday.$dirty && !$v.birthday.required"
            >обязательно для заполнения</small>
            <small
              class="helper-text invalid"
              v-else-if="$v.birthday.$dirty && $v.birthday.$validDate"
            >дата в формате ДД.ММ.ГГГГ</small>
          </div>

          <div 
            class="input-field" 
            :class="{invalid: ($v.phone.$dirty && !$v.phone.validPhone)}"
          >
            <label class="input-label">Номер телефона</label>
            <input 
              type="number"
              name="phone" 
              v-model="phone" 
            >
            <small
              class="helper-text invalid"
              v-if="$v.phone.$dirty && !$v.phone.validPhone"
            >неверный формат</small>
          </div>

          <div class="input-field">
            <label class="input-label">Пол</label>
            <div class="radio-buttons">
              <label class="radio-buttons__label">мужчина
                <input class="radio-buttons__input" type="radio" name="sex" checked="checked">
                <div class="radio-buttons__marker"></div>
              </label>
              <label class="radio-buttons__label">женщина
                <input class="radio-buttons__input" type="radio" name="sex">
                <div class="radio-buttons__marker"></div>
              </label>
            </div>
          </div>

          <div 
            class="input-field" 
            :class="{invalid: ($v.groups.$dirty && !$v.groups.required)}"
          >
            <label class="input-label required-label">Группа клиентов</label>
            <select multiple name="groups[]" v-model="groups">
              <option value="VIP">VIP</option>
              <option value="Проблемные">Проблемные</option>
              <option value="ОМС">ОМС</option>
            </select>
            <small
              class="helper-text invalid"
              v-if="$v.groups.$dirty && !$v.groups.required"
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
            <label class="checkbox">Не отправлять СМС
              <input class="checkbox__input" type="checkbox" name="sms" v-model="sms">
              <div class="checkbox__marker"></div>
            </label>
          </div>


        </div>

        <div class="address">
          <h3>Адрес</h3>

          <div class="input-field">
            <label class="input-label">Индекс</label>
            <input type="text" name="index">
          </div>

          <div class="input-field">
            <label class="input-label">Страна</label>
            <input type="text" name="country">
          </div>

          <div class="input-field">
            <label class="input-label">Область</label>
            <input type="text" name="area">
          </div>

          <div 
            class="input-field" 
            :class="{invalid: ($v.city.$dirty && !$v.city.required)}"
          >
            <label class="input-label required-label">Город</label>
            <input type="text" name="city"           
              v-model.trim="city" 
            >
            <small
              class="helper-text invalid"
              v-if="$v.city.$dirty && !$v.city.required"
            >обязательно для заполнения</small>
          </div>

          <div class="input-field">
            <label class="input-label">Улица</label>
            <input type="text" name="street">
          </div>

          <div class="input-field">
            <label class="input-label">Дом</label>
            <input type="text" name="house">
          </div>

        </div>


        <div class="passport">      
          <h3>Паспорт</h3>

          <div 
            class="input-field" 
            :class="{invalid: ($v.documents.$dirty && !$v.documents.required)}"
          >
            <label class="input-label required-label">Тип документа</label>
            <select name="documents[]" v-model="documents" >
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
            <input type="number" name="series">
          </div>

          <div class="input-field">
            <label class="input-label">Номер</label>
            <input type="number" name="number">
          </div>

          <div 
            class="input-field" 
            :class="{invalid: ($v.dateOfIssue.$dirty && !$v.dateOfIssue.required) || ($v.dateOfIssue.$dirty && $v.dateOfIssue.$validDate)}"
          >
            <label class="input-label required-label">Дата выдачи</label>
            <input 
              type="text" 
              name="dateOfIssue" 
              v-model="dateOfIssue" 
            >
            <small
              class="helper-text invalid"
              v-if="$v.dateOfIssue.$dirty && !$v.dateOfIssue.required"
            >обязательно для заполнения</small>
            <small
              class="helper-text invalid"
              v-else-if="$v.dateOfIssue.$dirty && $v.dateOfIssue.$validDate"
            >дата в формате ДД.ММ.ГГГГ</small>
          </div>
        </div>

      </div>

      <div class="btn__wrapper">
        <button class="btn-create">Создать</button>
      </div>

    </form>
  </div>
</template>

<script>
import Popup from './Popup'
import {required, minLength} from 'vuelidate/lib/validators';
import {valdate, floatRegExp} from './validHelpers'

export default {
  name: 'register',
  components: {
    Popup
  },
  data: () => ({
    isPopupVisible: false,
    lastname: '',
    firstname: '',
    birthday: '',
    phone: '',
    groups: [],
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
    groups: {required},
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
      this.isPopupVisible = true
    },
    closePopup() {
      this.isPopupVisible = false
    }
  }
}
</script>

<style lang="scss" scoped>
$primary: #2c3e50;
$error: #f57f6c;

.register__form {
  padding: 2rem 5rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.register__form-wrapper{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  width: 60%;
  max-width: 800px;

  @media(max-width: 870px) {
    justify-content: center;
  }
}
.input-field {
  display: flex;
  position: relative;
  flex-direction: column;
  margin-bottom: 2rem;
}
.input-label {
  min-width: 200px;
  position: relative;
  text-align: left;
  line-height: 22px;
  padding: 0 4px;
}
input {
  padding: 4px 6px;
  border: 1px solid $primary;
  border-radius: 5px;
}
.invalid input,
.invalid input:focus {
  border: 1px solid $error;
  animation-name: shakeError;
  animation-fill-mode: forwards;
  animation-duration: .6s;
  animation-timing-function: ease-in-out;
}
input:focus{
  outline: none;
}
.radio-buttons {
  &__label {
    position: relative;
    margin-right: 20px;
    padding-left: 30px;
    cursor: pointer;
  }

  &__input:checked,
  &__input:not(:checked) {
    display:none;
  }

  &__input:checked ~ &__marker::after {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 12px;
    height: 12px;
    box-sizing: border-box;
    background: $primary;
    border-radius: 100%;
  }
  &__marker {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 20px;
    height: 20px;
    border-radius: 100%;
    border: 1px solid $primary;
    box-sizing: border-box;
  }
}

.checkbox {
  display: block;
  position: absolute;
  padding-left: 30px;
  cursor: pointer;
  user-select: none;
  line-height: 22px;
  color: $primary;

  &__input[type='checkbox'] {
    display: none;
  }

  &__marker {
    position: absolute;
    top: 0;
    left: 0;
    width: 20px;
    height: 20px;
    border: 1px solid $primary;
    border-radius: 0.25em;
  }

  &__marker::after {
    content: '';
    display: none;
    position: absolute;
    top: 4px;
    left: 6px;
    width: 6px;
    height: 8px;
    border-width: 0 2px 2px 0;
    border-style: solid;
    border-color: $primary;
    transform: rotate(45deg);
  }

  &__input:checked + &__marker {
    border-color: $primary;
  }

  &__input:checked + &__marker::after {
    display: block;
  }
}
select {
  padding: 3px 6px;
  border: 1px solid $primary;
  border-radius: 5px;
  overflow-y: hidden;
}
.invalid select,
.invalid select {
  border: 1px solid $error;
  animation-name: shakeError;
  animation-fill-mode: forwards;
  animation-duration: .6s;
  animation-timing-function: ease-in-out;
}
select:focus{
  outline: none;
}
.helper-text.invalid {
  position: absolute;
  bottom: -20px;
  color: $error;
  padding: 0 4px;
}
.required-label::after {
  content: '\2732';
  color: $error;
  top: -4px;
  font-size: 10px;
  position: absolute;
}

.btn-create {
  padding: 10px 18px;
  font-size: 1.2rem;
  text-transform: uppercase;
  letter-spacing: 2.5px;
  border-radius: 45px;
  border: none;
  cursor: pointer;
  background: #fff;
  box-shadow: 0px 8px 15px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease 0s;
  outline: none;
}
.btn-create:hover {
  background-color: #2EE59D;
  box-shadow: 0px 15px 20px rgba(46, 229, 157, 0.4);
  color: #fff;
  transform: translateY(-7px);
}
.btn-create:active {
  transform: translateY(7px);
}

@keyframes shakeError {
  0% {
    transform: translateX(0);
  }
  15% {
      transform: translateX(0.375rem);
  }
  30% {
      transform: translateX(-0.375rem);
  }
  45% {
      transform: translateX(0.375rem);
  }
  60% {
      transform: translateX(-0.375rem);
  }
  75% {
      transform: translateX(0.375rem);
  }
  90% {
      transform: translateX(-0.375rem);
  }
  100% {
      transform: translateX(0);
  }
}
</style>