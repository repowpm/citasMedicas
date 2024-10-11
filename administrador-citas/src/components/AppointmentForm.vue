<template>
  <div class="form-container">
    <form @submit.prevent="submitForm" class="form-horizontal">
      <div class="form-group">
        <label :class="{ 'red-label': !patient }">Paciente:</label>
        <input type="text" v-model="patient" />
      </div>
      <div class="form-group">
        <label :class="{ 'red-label': !date }">Fecha:</label>
        <input type="date" v-model="date" />
      </div>
      <div class="form-group">
        <label :class="{ 'red-label': !time }">Hora:</label>
        <input type="time" v-model="time" />
      </div>
      <div class="form-group">
        <label :class="{ 'red-label': !severity }">Gravedad:</label>
        <select v-model="severity">
          <option disabled value="">Selecciona una opción</option>
          <option value="Baja">Baja</option>
          <option value="Media">Media</option>
          <option value="Alta">Alta</option>
        </select>
      </div>
      <div class="form-group">
        <label :class="{ 'red-label': !reason }">Motivo:</label>
        <input type="text" v-model="reason" />
      </div>
      <div class="form-group">
        <button :disabled="!isFormValid">Agregar cita</button>
      </div>
    </form>

    <p v-if="appointments.length === 0">Aún no hay consultas registradas</p>

    <div class="appointments-container">
      <h2>Citas Registradas</h2>
      <div class="appointments-grid">
        <div v-for="(appointment, index) in appointments" :key="index">
          <AppointmentCard :appointment="appointment" @remove="removeAppointment(index)" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AppointmentCard from './AppointmentCard.vue';

export default {
  components: {
    AppointmentCard,
  },
  data() {
    return {
      patient: "",
      date: "",
      time: "",
      severity: "",
      reason: "",
      appointments: [], 
    };
  },
  computed: {
    isFormValid() {
      return this.patient && this.date && this.time && this.severity && this.reason;
    },
  },
  methods: {
    submitForm() {
      if (this.isFormValid) {
        const newAppointment = {
          patient: this.patient,
          date: this.date,
          time: this.time,
          severity: this.severity,
          reason: this.reason,
        };

        this.appointments.push(newAppointment);

        this.patient = "";
        this.date = "";
        this.time = "";
        this.severity = "";
        this.reason = "";
      }
    },
    removeAppointment(index) {
      this.appointments.splice(index, 1);
    },
  },
};
</script>

<style scoped>
.red-label {
  color: red;
}


.form-container {
  display: flex;
  flex-direction: column;
  align-items: center; 
  justify-content: center; 
  border: 2px solid #ccc; 
  border-radius: 8px; 
  padding: 1.5rem; 
  margin: 2rem; 
  width: 90%; 
  max-width: 100%;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); 
}

.form-horizontal {
  display: flex;
  flex-wrap: wrap; 
  gap: 1rem; 
  align-items: center; 
}

.form-group {
  display: flex;
  flex-direction: column; 
  margin: 0; 
  min-width: 120px; 
}

button {
  margin-top: 1rem;
  padding: 0.5rem 1rem;
}

.appointments-container {
  display: flex; 
  flex-direction: column; 
  align-items: center; 
  width: 100%; 
  margin-top: 2rem; 
}

.appointments-grid {
  display: flex; 
  flex-wrap: wrap;
  justify-content: center; 
  gap: 1rem; 
  width: 100%; 
}
</style>
