<template>
  <div class="app" id="app">
    <h1 class="app__title">Создание клиента</h1>
    <MainForm />
  </div>
</template>

<script>
import MainForm from './components/MainForm.vue';

export default {
  name: 'App',
  components: {
    MainForm
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
