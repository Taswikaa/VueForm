<template>
  <form
    class="form"
    ref="form"
    @submit.prevent="() => sendForm(form)"
  >
    <div class="form__wrapper">
      <h2 class="form__title">Основная информация</h2>
      <div class="form__part">
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Фамилия</h4>
          <input 
            class="form__input" 
            type="text"
            v-model.trim="form.main.surname"
            @input="$v.form.main.surname.$touch()"
            @keydown="(e) => allowOnlyWordInput(e)"
          >
          <p
            class="form__error"
            :class="{'form__error_visible': $v.form.main.surname.$error && $v.form.main.surname.$dirty}"
          >
            Обязательное поле
          </p>
        </label>
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Имя</h4>
          <input 
            class="form__input" 
            type="text"
            v-model.trim="form.main.name"
            @input="$v.form.main.name.$touch()"
            @keydown="(e) => allowOnlyWordInput(e)"
          >
          <p
            class="form__error"
            :class="{'form__error_visible': $v.form.main.name.$error && $v.form.main.name.$dirty}"
          >
            Обязательное поле
          </p>
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Отчество</h4>
          <input
            class="form__input"
            type="text"
            v-model.trim="form.main.patronymic"
            @keydown="(e) => allowOnlyWordInput(e)"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Дата рождения</h4>
          <input 
            class="form__input" 
            type="date"
            v-model="form.main.dateOfBirth"
            @input="$v.form.main.dateOfBirth.$touch()"
          >
          <p
            class="form__error"
            :class="{'form__error_visible': $v.form.main.dateOfBirth.$error && $v.form.main.dateOfBirth.$dirty}"
          >
            Обязательное поле
          </p>
        </label>
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory form__field-title_phone">Номер телефона</h4>
          <input
            class="form__input form__input_phone"
            type="text"
            :maxlength="10"
            v-model="form.main.phone"
            @input="$v.form.main.phone.$touch()"
            @keydown="(e) => allowOnlyNumberInput(e)"
          >
          <p
            v-if="!$v.form.main.phone.$model.length > 0"
            class="form__error"
            :class="{'form__error_visible': $v.form.main.phone.$error && $v.form.main.phone.$dirty}"
          >
            Обязательное поле
          </p>
          <p
            v-else
            class="form__error"
            :class="{'form__error_visible': $v.form.main.phone.$error}"
          >
            Введите номер без 7, 10 цифр
          </p>
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Пол</h4>
          <div class="form__field_radio">
            <div class="">
              <input 
                class="form__radio" 
                type="radio" 
                name="gender"
                value="Мужчина"
                v-model="form.main.gender"
              ><p>Мужчина</p>
            </div>
            <div class="">
              <input 
                class="form__radio" 
                type="radio" 
                name="gender"
                value="Женщина"
                v-model="form.main.gender"
              ><p>Женщина</p>
            </div>
          </div>
        </label>
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Группа клиентов</h4>
          <select
            class="form__select"
            multiple
            v-model="form.main.clientsGroup"
            @change="$v.form.main.clientsGroup.$touch()"
          >
            <option
              v-for="(type, i) in clientsGroup"
              :value="type.value"
              :key="i"
            >
              {{ type.label }}
            </option>
          </select>
          <p
            class="form__error"
            :class="{'form__error_visible': $v.form.main.clientsGroup.$error && $v.form.main.clientsGroup.$dirty}"
          >
            Обязательное поле
          </p>
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Лечащий врач</h4>
          <select class="form__select" v-model="form.main.doctor">
            <option
              v-for="(doctor, i) in doctors"
              :value="doctor.value"
              :key="i"
            >
              {{ doctor.label }}
            </option>
          </select>
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Не отправлять СМС</h4>
          <input
            class="form__check"
            type="checkbox"
            v-model="form.main.doNotSendSms"
          >
        </label>
      </div>
    </div>
    <div class="form__wrapper">
      <h2 class="form__title">Адрес</h2>
      <div class="form__part">
        <label class="form__field">
          <h4 class="form__field-title">Индекс</h4>
          <input
            class="form__input"
            type="text"
            maxlength="6"
            v-model="form.address.postcode"
            @keydown="(e) => allowOnlyNumberInput(e)"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Страна</h4>
          <input
            class="form__input"
            type="text"
            v-model.trim="form.address.country"
            @keydown="(e) => allowOnlyWordInput(e)"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Область</h4>
          <input
            class="form__input"
            type="text"
            v-model.trim="form.address.area"
            @keydown="(e) => allowOnlyWordInput(e)"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Город</h4>
          <input
            class="form__input"
            type="text"
            v-model.trim="form.address.city"
            @input="$v.form.address.city.$touch()"
            @keydown="(e) => allowOnlyWordInput(e)"
          >
          <p
            class="form__error"
            :class="{'form__error_visible': $v.form.address.city.$error && $v.form.address.city.$dirty}"
          >
            Обязательное поле
          </p>
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Улица</h4>
          <input
            class="form__input"
            type="text"
            v-model.trim="form.address.street"
            @keydown="(e) => allowOnlyWordInput(e)"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Дом</h4>
          <input
            class="form__input"
            type="text"
            v-model.trim="form.address.home"
          >
        </label>
      </div>
    </div>
    <div class="form__wrapper">
      <h2 class="form__title">Документы</h2>
      <div class="form__part">
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Тип документа</h4>
          <select
            class="form__select"
            v-model="form.documents.type"
          >
            <option
              v-for="(type, i) in allowedDocuments"
              :value="type.value"
              :key="i"
            >
              {{ type.label }}
            </option>
          </select>
          <p
            class="form__error"
            :class="{'form__error_visible': $v.form.documents.type.$error && $v.form.documents.type.$dirty}"
          >
            Обязательное поле
          </p>
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Серия</h4>
          <input
            class="form__input"
            type="text"
            v-model="form.documents.series"
            @keydown="(e) => allowOnlyNumberInput(e)"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Номер</h4>
          <input
            class="form__input"
            type="text"
            v-model="form.documents.number"
            @keydown="(e) => allowOnlyNumberInput(e)"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Кем выдан</h4>
          <input
            class="form__input"
            type="text"
            v-model.trim="form.documents.pickUpPoint"
            @keydown="(e) => allowOnlyWordInput(e)"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Дата выдачи</h4>
          <input
            class="form__input"
            type="date"
            @input="$v.form.documents.date.$touch()"
            v-model="form.documents.date"
          >
          <p
            class="form__error"
            :class="{'form__error_visible': $v.form.documents.date.$error && $v.form.documents.date.$dirty}"
          >
            Обязательное поле
          </p>
        </label>
      </div>
    </div>
    <button
      class="button form__button"
      :class="{'form__button_disabled' : !$v.form.$anyDirty || $v.form.$anyError }"
      :disabled="!$v.form.$anyDirty || $v.form.$anyError ? true : false"
    >Создать</button>
  </form>
</template>

<script>
  import { validationMixin } from 'vuelidate'
  import { required, minLength, maxLength } from 'vuelidate/lib/validators'

 export default {
  name: 'MainForm',
  mixins: [validationMixin],
  validations: {
    form: {
      main: {
        surname: { required },
        name: { required },
        dateOfBirth: { required },
        phone: { required, minLength: minLength(10) },
        clientsGroup: { required },
      },
      address: {
        city: { required }
      },
      documents: {
        type: { required },
        date: { required }
      }
    }
  },
  data() {
    return {
      form: {
        main: {
          surname: '',
          name: '',
          patronymic: '',
          dateOfBirth: '',
          phone: '',
          gender: '',
          clientsGroup: [],
          doctor: 'Врач не назначен',
          doNotSendSms: false
        },
        address: {
          postcode: '',
          country: '',
          area: '',
          city: '',
          street: '',
          home: '',
        },
        documents: {
          type: 'Паспорт',
          series: '',
          number: '',
          pickUpPoint: '',
          date: '',
        }
      },
      clientsGroup: [
        {
          label: 'VIP',
          value: 'VIP'
        },
        {
          label: 'Проблемные',
          value: 'Проблемные'
        },
        {
          label: 'ОМС',
          value: 'ОМС'
        },
      ],
      doctors: [
        {
          label: 'Иванов',
          value: 'Иванов'
        },
        {
          label: 'Захаров',
          value: 'Захаров'
        },
        {
          label: 'Чернышёва',
          value: 'Чернышёва'
        },
        {
          label: 'Врач не назначен',
          value: 'Врач не назначен'
        },
      ],
      allowedDocuments: [
        {
          label: 'Паспорт',
          value: 'Паспорт'
        },
        {
          label: 'Свидетельство о рождении',
          value: 'Свидетельство о рождении'
        },
        {
          label: 'Вод. удостоверение',
          value: 'Вод. удостоверение'
        },
      ]
    }
  },
  methods: {
    allowOnlyNumberInput(e) {
      if (isNaN(e.key) && e.key !== 'Backspace') {
        e.preventDefault();
      }
      if (e.key == ' ') e.preventDefault();
    },
    allowOnlyWordInput(e) {
      if (!isNaN(e.key) && e.key !== 'Backspace' && e.key !== ' ') {
        e.preventDefault();
      }
    },
    sendForm(data) {
      this.$v.form.$touch()
      if (!this.$v.form.$error) {
        this.$emit('getData', data);
        this.$refs.form.reset();
        this.$v.form.$reset();
        this.form = {
          main: {
            surname: '',
            name: '',
            patronymic: '',
            dateOfBirth: '',
            phone: '',
            gender: '',
            clientsGroup: [],
            doctor: 'Врач не назначен',
            doNotSendSms: false
          },
          address: {
            postcode: '',
            country: '',
            area: '',
            city: '',
            street: '',
            home: '',
          },
          documents: {
            type: 'Паспорт',
            series: '',
            number: '',
            pickUpPoint: '',
            date: '',
          }
        }
      }
    }
  }
}
</script>

<style scoped lang="scss">
  @import '@/styles/index.scss';
  .form {
    @include vertical-layout;
    padding: 1.5rem 0;
    min-width: 18rem;
    background-color: $emphasizing-color;
    border-radius: 1rem;

    &__title {
      font-weight: 500;
      font-size: 1.5rem;
      margin-bottom: 1.5rem;
    }

    &__error {
      color: $error-color;
      align-self: flex-start;
      display: none;

      &_visible {
        display: block;
      }
    }

    &__part {
      @include vertical-layout;
      row-gap: 1.5rem;
      padding-bottom: 1rem;
    }

    &__field {
      @include vertical-layout;
      row-gap: .5rem;
      min-width: 13rem;
      position: relative;

      &_align_horizontal {
        flex-direction: row;
      }

      &_radio {
        display: flex;
        align-self: flex-start;
        margin-left: .25rem;
        column-gap: 1rem ;
      }
    }

    &__field-title {
      font-weight: 400;
      font-size: 1.25rem;
      align-self: flex-start;
      margin-left: .25rem;
      position: relative; 

      &_mandatory {
        font-weight: 700;
      }

      &_phone {
        &::after {
          content: '+7';
          position: absolute;
          padding: 0.25rem;
          top: 1.9rem;
          left: 0;
          font-size: 1.1rem;
          opacity: .7;
        }
      }
    }

    &__input {
      @include basic-input;
      align-self: flex-start;

      &_phone {
        max-width: 205px;
        padding-left: 2rem;
      }
    }

    &__check {
      position: absolute;
      top: .27rem;
      right: 0;
    }

    &__select {
      @include basic-input;
      align-self: flex-start;
      width: 13rem;
    }

    &__button {
      min-width: 13rem;
      margin-top: 0.5rem;

      &_disabled {
        opacity: .5;
        color: #000;
      }
    }
  }

  @media screen and (min-width: 1024px) {
    .form {
      min-width: 58rem;
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      align-items: flex-start;
      position: relative;
      padding-bottom: 0;

      &__wrapper {
        @include vertical-layout;
      }

      &__check {
        cursor: pointer;
      }
  
      &__select {
        cursor: pointer;
      }

      &__radio {
        cursor: pointer;
      }

      &__button {
        position: absolute;
        min-width: 18rem;
        border-radius: 1.5rem;
        font-size: 3rem;
        padding: 2rem;
        bottom: 6rem;
        left: 50%;
        cursor: pointer;
        margin: 0;

        &_disabled {
          cursor: default;
        }
      }
    }
  }
</style>