<template>
  <div id="app">
    <FormMain></FormMain>
  </div>
</template>

<script>
import FormMain from "./components/FormMain.vue";

export default {
  name: "App",
  components: {
    FormMain,
  },
};
</script>

<style>
#app {
  margin: 0 auto;
  padding: 150px 0;
  background-color: #f1f5fe;
}
@media (max-width: 768px) {
  #app {
    padding: 40px 20px;
  }
  .form__select {
    height: 40px;
  }
}
</style>
