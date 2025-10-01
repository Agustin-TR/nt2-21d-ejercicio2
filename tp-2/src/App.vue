<template>
  <div class="container-fluid mt-3">
    <input
      type="text"
      class="form-control"
      v-model="filtroNombreCompleto"
      placeholder="Ingresar nombre completo..."
    />
    <input
      type="text"
      class="form-control"
      v-model="filtroDni"
      placeholder="Ingresar dni..."
    />
    <div
      v-if="(filtroNombreCompleto.length > 0 && filtroNombreCompleto.length < 3) || (filtroDni.length > 0 && filtroDni.length < 3)"
      class="alert alert-warning mt-2"
    >
      Ingresá al menos 3 caracteres en alguno de los filtros.
    </div>

    <br />
    <div class="card-deck m-0">
      <div class="row">
        <div class="col" v-for="persona in personasFiltradas" :key="persona.dni">
          <div class="card mb-3">
            <div class="card-body">
              <h5 class="card-title">{{ getNombreCompleto(persona) }}</h5>
              <p class="card-text">dni {{ persona.dni }}</p>
              <a href="#" class="card-link">{{ persona.correo }}</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      filtroNombreCompleto: '',
      filtroDni: '',
      personas: [
        { nombre: 'Daniel', apellido: 'Sanchez', correo: 'danielsanchez68@hotmail.com', dni: '20442873' },
        { nombre: 'Juan', apellido: 'Perez', correo: 'j@p.gmail.com', dni: '12345678' },
        { nombre: 'Agustin', apellido: 'Rojas', correo: 'a@s.gmail.com', dni: '87654321' },
        { nombre: 'Agustin', apellido: 'Rojas', correo: 'agus@gmail.com', dni: '123432123' },
      ],
    };
  },
  computed: {
    personasFiltradas() {
      const nombreValido = this.filtroNombreCompleto.length >= 3;
      const dniValido = this.filtroDni.length >= 3;

      if (!nombreValido && !dniValido) return this.personas;

      return this.personas.filter((persona) => {
        const nombreCompleto = `${persona.nombre} ${persona.apellido}`.toLowerCase();
        const dni = `${persona.dni}`;
        const coincideDni = dniValido ? dni.includes(this.filtroDni.toLowerCase()) : true;
        const coincideNombre = nombreValido ? nombreCompleto.includes(this.filtroNombreCompleto.toLowerCase()) : true;
        return coincideNombre && coincideDni;
      });
    },
  },
  methods: {
    getNombreCompleto(persona) {
      return `${persona.nombre} ${persona.apellido}`;
    },
  },
};
</script>

<style>
@import 'https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css';
</style>
