<template>
  <div id="app">
    <h1>Administrador de citas médicas</h1>
    <AppointmentForm />
  </div>
</template>

<script>
import AppointmentForm from './components/AppointmentForm.vue';

export default {
  components: {
    AppointmentForm,
  },
};
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 20px;
}
</style>

