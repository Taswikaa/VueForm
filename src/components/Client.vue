<template>
  <div class="client" ref="form" :class='{visible: isActive}'>
    <button class="close-button" @click="close"></button>
    <h2 class="client__heading">Клинент создан</h2>
    <div class="client__info">
      <div class="client__info-block">
        <h3 class="client__info-heading">Данные:</h3>
        <ul class="client__info-list">
          <li>Фамилия: {{ formData.main.surname }}</li>
          <li>Имя: {{ formData.main.name }}</li>
          <li>Отчество: {{ formData.main.patronymic }}</li>
          <li>Дата рождения: {{ formData.main.dateOfBirth }}</li>
          <li>Телефон: +7{{ formData.main.phone }}</li>
          <li>Пол: {{ formData.main.gender }}</li>
          <li>Группа: {{ formData.main.clientsGroup }}</li>
          <li>Врач: {{ formData.main.doctor }}</li>
          <li v-if="formData.main.doNotSendSms">Не отправлять SMS</li>
          <li v-else>Отправлять SMS</li>
        </ul>
      </div>
      <div class="client__info-block">
        <h3 class="client__info-heading">Адрес:</h3>
        <ul class="client__info-list">
          <li>Индекс: {{ formData.address.postcode }}</li>
          <li>Страна: {{ formData.address.country }}</li>
          <li>Область: {{ formData.address.area }}</li>
          <li>Город: {{ formData.address.city }}</li>
          <li>Улица: {{ formData.address.street}}</li>
          <li>Дом: {{ formData.address.home }}</li>
        </ul>
      </div>
      <div class="client__info-block">
        <h3 class="client__info-heading">Документы:</h3>
        <ul class="client__info-list">
          <li>Тип: {{ formData.documents.type }}</li>
          <li>Серия: {{ formData.documents.series }}</li>
          <li>Номер: {{ formData.documents.number }}</li>
          <li>Выдан: {{ formData.documents.pickUpPoint }}</li>
          <li>Дата выдачи: {{ formData.documents.date }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Client',
  props: ['isActive', 'formData'],
  methods: {
    close() {
      this.$emit('close');
    }
  }
}
</script>

<style scoped lang="scss">
  @import '@/styles/index.scss';

  .client {
    @include vertical-layout;
    padding: 1rem;
    position: absolute;
    width: 18rem;
    border: 1px solid black;
    z-index: 10;
    background-color: $second-color;
    color: $emphasizing-color;
    font-size: 1.5rem;
    border-radius: 1rem;
    display: none;

    &__heading {
      font-size: 2rem;
      margin-bottom: 1.5rem;
      font-weight: 500;
    }

    &__info {
      @include vertical-layout;
      align-items: flex-start;
      min-width: 100%;
      row-gap: 1.5rem;

      &-heading {
        font-weight: 400;
        font-size: 2rem;
        color: $main-color;
        margin-bottom: 1rem;
      }

      &-list {
        list-style: none;
        font-size: 1.25rem;
        @include vertical-layout;
        align-items: flex-start;
        row-gap: .8rem;
      }
    }
  }

  .visible {
    display: flex;
  }

  .close-button {
    position: absolute;
    right: .5rem;
    top: .5rem;
    border: none;
    width: 1.5rem;
    height: 1.5rem;
    background-color: transparent;

    &::after {
      content: '';
      position: absolute;
      width: 1.5rem;
      height: .25rem;
      background-color: $main-color;
      top: 50%;
      left: 0;
      transform: rotate(-45deg);
    }

    &::before {
      content: '';
      position: absolute;
      width: 1.5rem;
      height: .25rem;
      background-color: $main-color;
      top: 50%;
      left: 0;
      transform: rotate(45deg);
    }
  }

  @media screen and (min-width: 1024px) {
    .client {
      width: 60rem;
      padding: 3rem 1.5rem;

      &__info {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
      }
    }

    .close-button {
      cursor: pointer;
    }
  }
</style>