<template>
  <div :class="['card', severityClass]">
    <h3>{{ appointment.patient }}</h3>
    <p>Fecha: {{ appointment.date }}</p>
    <p>Hora: {{ appointment.time }}</p>
    <p>Gravedad: {{ appointment.severity }}</p>
    <p>Motivo: {{ appointment.reason }}</p>
    <button @click="removeAppointment">Eliminar</button>
  </div>
</template>

<script>
export default {
  props: {
    appointment: Object,
  },
  computed: {
    severityClass() {
      if (this.appointment.severity === 'Alta') return 'high-severity';
      if (this.appointment.severity === 'Media') return 'medium-severity';
      return 'low-severity';
    },
  },
  methods: {
    removeAppointment() {
      this.$emit('remove', this.appointment);
    },
  },
};
</script>

<style scoped>
.card {
  border: 1px solid #ccc; 
  padding: 1rem; 
  margin: 1rem; 
  border-radius: 8px; 
  width: 100%; 
}

.high-severity {
  background-color: red; 
}

.medium-severity {
  background-color: yellow 
}

.low-severity {
  background-color: green; 
}
</style>
