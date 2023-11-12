<template>
  <div class="app" id="app">
    <h1 class="app__title">Создание клиента</h1>
    <MainForm @getData="loadData" />
    <Client
      :isActive="isClientActive"
      @close="close"
      :formData="formData"
    />
  </div>
</template>

<script>
import MainForm from './components/MainForm.vue';
import Client from './components/Client.vue';

const defaultUser = {
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

export default {
  name: 'App',
  components: {
    MainForm,
    Client
  },
  data() {
    return {
      isClientActive: false,
      formData: Object.assign({}, defaultUser)
    }
  },
  methods: {
    loadData(data) {
      this.formData = data;
      this.isClientActive = true;
    },
    close() {
      this.isClientActive = false;
      this.formData = Object.assign({}, defaultUser);
    }
  }
}
</script>

<style lang="scss">
  @import '@/styles/index.scss';

  * {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .app {
    @include vertical-layout;
    min-height: 100vh;
    background-color: $main-color;
    color: $second-color;
    font-size: $basic-font-size;
    padding-top: 1.5rem;
    position: relative;

    &__title {
      font-size: 2rem;
      font-weight: 500;
      margin-bottom: 1.5rem;
    }
  }

  .button {
    background-color: $main-color;
    border: none;
    padding: .5rem;
    border-radius: .5rem;
    color: $second-color;
  }
</style>
