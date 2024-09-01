<!-- Script JS -->
<script>
export default {
  name: "CardCita", // Nombre del componente, utilizado para su referencia dentro de otros componentes
  props: {
    // Definición de las propiedades que recibe el componente desde el padre
    cita: Object, // La propiedad 'cita' es un objeto que contiene los detalles de la cita médica
  },
  computed: {
    // Computed property para determinar la clase de fondo según la gravedad de la cita
    bgGravedad() {
      // Mapeo de los niveles de gravedad a clases CSS específicas de Bootstrap
      const clasesGravedad = {
        Baja: "bg-success", // Clase para gravedad baja (verde)
        Media: "bg-warning", // Clase para gravedad media (amarillo)
        Alta: "bg-danger", // Clase para gravedad alta (rojo)
      };
      // Retorna la clase correspondiente según la gravedad de la cita
      return clasesGravedad[this.cita.gravedad];
    },
  },
};
</script>


<!-- Template HTML -->
<template>
  <!-- Contenedor principal de la tarjeta de cita médica -->
  <!-- Aplicación dinámica de clases según la gravedad de la cita -->
  <article class="card text-center" :class="bgGravedad">
    <div class="card-body">
      <h5 class="card-title">Paciente</h5>
      <!-- Muestra el nombre del paciente -->
      <p class="card-text">{{ cita.paciente }}</p>
      <h5 class="card-title">Fecha</h5>
      <!-- Muestra la fecha de la cita -->
      <p class="card-text">{{ cita.fecha }}</p>
      <h5 class="card-title">Hora</h5>
      <!-- Muestra la hora de la cita -->
      <p class="card-text">{{ cita.hora }}</p>
      <h5 class="card-title">Motivo</h5>
      <!-- Muestra el motivo de la cita -->
      <p class="card-text">{{ cita.motivo }}</p>
      <!-- Botón para eliminar la cita, emite un evento 'eliminarCita' al hacer clic -->
      <button class="btn btn-primary" @click="$emit('eliminarCita')">Eliminar</button>
    </div>
  </article>
</template>