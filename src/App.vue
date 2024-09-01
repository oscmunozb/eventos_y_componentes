<!-- Script JS -->
<script>
import CardCita from "./components/CardCita.vue"; // Importa el componente CardCita para poder usarlo 

export default {
  name: "App", // Nombre del componente principal de la aplicación
  data() {
    return {
      // Estado inicial de la aplicación
      citas: [], // Array para almacenar las citas médicas
      cita: { // Objeto para almacenar los datos de la cita actual
        paciente: '', // Nombre del paciente
        fecha: '', // Fecha de la cita
        hora: '', // Hora de la cita
        gravedad: '', // Gravedad de la cita
        motivo: '', // Motivo de la cita
      },
      gravedades: ['Baja', 'Media', 'Alta'], // Opciones de gravedad disponibles para seleccionar
    };
  },
  methods: {
    // Método para agregar una nueva cita al array 'citas'
    agregarCita() {
      this.citas.push(this.cita); // Agrega la cita actual al array de citas
      this.cita = {}; // Resetea el objeto 'cita' para permitir la creación de una nueva cita
    },
    // Método para eliminar una cita específica del array 'citas'
    procesarEliminacionCita(index) {
      this.citas.splice(index, 1); // Elimina la cita en la posición especificada del array
    }
  },
  components: {
    CardCita, // Registro del componente CardCita para su uso en el template
  },
}
</script>


<!-- Template HTML -->
<template>
  <section class="container">
    <h1 class="text-center mt-3 mb-4">Administrador de citas médicas.</h1>

    <!-- Formulario para ingresar los datos de una nueva cita -->
    <form class="border border-black rounded-4 mb-5" @submit.prevent="agregarCita">
      <div class="d-md-flex flex-wrap justify-content-around m-4 text-center">
        <!-- Campo de entrada para el nombre del paciente -->
        <div>
          <label class="form-label fw-bold" :class="cita.paciente ? 'text-black' : 'text-danger'"
            for="paciente">Paciente</label>
          <input class="form-control" type="text" id="paciente" v-model="cita.paciente">
        </div>
        <!-- Campo de entrada para la fecha de la cita -->
        <div>
          <label class="form-label fw-bold" :class="cita.fecha ? 'text-black' : 'text-danger'" for="fecha">Fecha</label>
          <input class="form-control" type="date" id="fecha" v-model="cita.fecha">
        </div>
        <!-- Campo de entrada para la hora de la cita -->
        <div>
          <label class="form-label fw-bold" :class="cita.hora ? 'text-black' : 'text-danger'" for="hora">Hora</label>
          <input class="form-control" type="time" id="hora" v-model="cita.hora">
        </div>
        <!-- Campo de selección para la gravedad de la cita -->
        <div>
          <label class="form-label fw-bold" :class="cita.gravedad ? 'text-black' : 'text-danger'"
            for="gravedad">Gravedad</label>
          <select class="form-select" id="gravedad" v-model="cita.gravedad">
            <!-- Opciones de gravedad generadas dinámicamente -->
            <option v-for="gravedad in gravedades" :value="gravedad">
              {{ gravedad }}
            </option>
          </select>
        </div>
        <!-- Campo de entrada para el motivo de la cita -->
        <div>
          <label class="form-label fw-bold" :class="cita.motivo ? 'text-black' : 'text-danger'"
            for="motivo">Motivo</label>
          <input class="form-control" type="text" id="motivo" v-model="cita.motivo">
        </div>
      </div>
      <!-- Botón para agregar la cita -->
      <div class="text-center mt-5 mb-4">
        <button class="btn btn-primary"
          :disabled="!cita.paciente || !cita.fecha || !cita.hora || !cita.gravedad || !cita.motivo">
          Agregar
        </button>
      </div>
    </form>

    <!-- Mensaje mostrado cuando no hay citas registradas -->
    <div class="text-center" v-if="citas.length == 0">
      <h3 class="text-danger">Aún no hay consultas registradas</h3>
    </div>

    <!-- Sección para mostrar las citas registradas -->
    <div class="row g-4">
      <!-- Itera sobre las citas y muestra una tarjeta para cada una -->
      <div class="col-12 col-sm-6 col-md-4 col-lg-3" v-for="(cita, index) in citas" :key="index">
        <!-- Muestra la información de la cita en el componente CardCita y maneja el evento de eliminar -->
        <CardCita :cita="cita" @eliminarCita="procesarEliminacionCita(index)" />
      </div>
    </div>
  </section>
</template>


<!-- Style CSS - scoped para asegurar que solo afecten a este componente -->
<style scoped>
</style>
