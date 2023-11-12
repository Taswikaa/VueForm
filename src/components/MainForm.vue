<template>
  <form class="form" @submit.prevent="sendForm">
    <div class="form__wrapper">
      <h2 class="form__title">Основная информация</h2>
      <div class="form__part">
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Фамилия</h4>
          <input 
            class="form__input" 
            type="text"
            v-model="form.main.surname"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Имя</h4>
          <input 
            class="form__input" 
            type="text"
            v-model="form.main.name"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Отчество</h4>
          <input
            class="form__input"
            type="text"
            v-model="form.main.patronymic"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Дата рождения</h4>
          <input 
            class="form__input" 
            type="date"
            v-model="form.main.dateOfBirth"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Номер телефона</h4>
          <input
            class="form__input"
            type="text"
            v-model="form.main.phone"
          >
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
          >
            <option
              v-for="(type, i) in clientsGroup"
              :value="type.value"
              :key="i"
            >
              {{ type.label }}
            </option>
          </select>
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
            v-model="form.address.postcode"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Страна</h4>
          <input
            class="form__input"
            type="text"
            v-model="form.address.country"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Область</h4>
          <input
            class="form__input"
            type="text"
            v-model="form.address.area"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Город</h4>
          <input
            class="form__input"
            type="text"
            v-model="form.address.city"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Улица</h4>
          <input
            class="form__input"
            type="text"
            v-model="form.address.street"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Дом</h4>
          <input
            class="form__input"
            type="text"
            v-model="form.address.home"
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
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Серия</h4>
          <input
            class="form__input"
            type="text"
            v-model="form.documents.series"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Номер</h4>
          <input
            class="form__input"
            type="text"
            v-model="form.documents.number"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Кем выдан</h4>
          <input
            class="form__input"
            type="text"
            v-model="form.documents.pickUpPoint"
          >
        </label>
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Дата выдачи</h4>
          <input
            class="form__input"
            type="date"
            v-model="form.documents.date"
          >
        </label>
      </div>
    </div>
    <button class="button form__button">Создать</button>
  </form>
</template>

<script>
export default {
  name: 'MainForm',
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
    sendForm() {
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
    }

    &__input {
      @include basic-input;
      align-self: flex-start;
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
      }
    }
  }
</style>