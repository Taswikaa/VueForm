<template>
  <form class="form">
    <div class="form__wrapper">
      <h2 class="form__title">Основная информация</h2>
      <div class="form__part">
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Фамилия</h4>
          <input class="form__input" type="text">
        </label>
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Имя</h4>
          <input class="form__input" type="text">
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Отчество</h4>
          <input class="form__input" type="text">
        </label>
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Дата рождения</h4>
          <input class="form__input" type="date">
        </label>
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Номер телефона</h4>
          <input class="form__input" type="text">
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Пол</h4>
          <div class="form__field_radio">
            <div class="">
              <input class="form__radio" type="radio" name="gender"> <p>Мужчина</p>
            </div>
            <div class="">
              <input class="form__radio" type="radio" name="gender"> <p>Женщина</p>
            </div>
          </div>
        </label>
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Группа клиентов</h4>
          <select class="form__select" name="" id="" multiple>
            <option value="">VIP</option>
            <option value="">Проблемные</option>
            <option value="">ОМС</option>
          </select>
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Лечащий врач</h4>
          <select class="form__select" name="" id="">
            <option value="">Иванов</option>
            <option value="">Захаров</option>
            <option value="">Чернышева</option>
          </select>
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Не отправлять СМС</h4>
          <input class="form__check" type="checkbox">
        </label>
      </div>
    </div>
    <div class="form__wrapper">
      <h2 class="form__title">Адрес</h2>
      <div class="form__part">
        <label class="form__field">
          <h4 class="form__field-title">Индекс</h4>
          <input class="form__input" type="text">
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Страна</h4>
          <input class="form__input" type="text">
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Область</h4>
          <input class="form__input" type="text">
        </label>
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Город</h4>
          <input class="form__input" type="text">
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Улица</h4>
          <input class="form__input" type="text">
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Дом</h4>
          <input class="form__input" type="text">
        </label>
      </div>
    </div>
    <div class="form__wrapper">
      <h2 class="form__title">Документы</h2>
      <div class="form__part">
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Тип документа</h4>
          <input class="form__input" type="text">
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Серия</h4>
          <input class="form__input" type="text">
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Номер</h4>
          <input class="form__input" type="text">
        </label>
        <label class="form__field">
          <h4 class="form__field-title">Кем выдан</h4>
          <input class="form__input" type="text">
        </label>
        <label class="form__field">
          <h4 class="form__field-title form__field-title_mandatory">Дата выдачи</h4>
          <input class="form__input" type="text">
        </label>
      </div>
    </div>
    <button class="button form__button">Создать</button>
  </form>
</template>

<script>
export default {
  name: 'MainForm'
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
      min-width: 13rem;
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