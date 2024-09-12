<template>
  <nav>
        <router-link to="/">Home</router-link> 
  </nav>
  <div class="container mt-5">
    <h2 class="mb-4">Reservar una cita</h2>

    <form @submit.prevent="crearCita">
      <div class="mb-3">
        <label for="doctor" class="form-label">Doctor</label>
        <select v-model="cita.doctor_id" @change="obtenerHorariosDoctor(cita.doctor_id)" class="form-select">
          <option value="" selected="true" >Selecciona un doctor</option>
          <option v-for="doctor in doctores" :key="doctor.id" :value="doctor.id">
            {{ doctor.nombre }}
          </option>
        </select>
      </div>

      <!-- Matriz de fechas y horarios -->
      <div v-if="fechasHorarios.length > 0" class="mb-3">
        <h4>Selecciona una fecha y horario</h4>
        <div class="row">
          <!-- Mostrar fechas y horarios -->
          <div v-for="(dia, index) in fechasAMostrar" :key="index" class="col-6 col-md-4 mb-3">
            <h5 class="text-center">{{ dia.dia }} {{ dia.fecha }}</h5>
            <div class="horarios-grid">
              <!-- Botones de horarios -->
              <button
                type="button"
                v-for="(horario, i) in dia.horarios"
                :key="i"
                :class="['btn', 'mb-2', horario.estado === 'ocupado' ? 'btn-danger' : 'btn-success']"
                :disabled="horario.estado === 'ocupado'"
                @click="seleccionarHorario(dia.fecha, horario)">
                {{ horario.hora_inicio }} - {{ horario.hora_fin }} ({{ horario.estado }})
              </button>
            </div>
          </div>
        </div>
      </div>

      <!-- Mostrar detalles del horario seleccionado -->
      <div v-if="horarioSeleccionado" class="mb-3">
        <h5>Has seleccionado:</h5>
        <p>Fecha: {{ horarioSeleccionado.fecha }} | Horario: {{ horarioSeleccionado.hora_inicio }} - {{ horarioSeleccionado.hora_fin }}</p>
      </div>

      <div class="mb-3">
        <label for="nombre" class="form-label">Nombre y Apellido</label>
        <input type="text" v-model="cita.nombre_cliente" class="form-control" placeholder="Nombre y Apellido" required>
      </div>

      <div class="mb-3">
        <label for="correo" class="form-label">Correo Electrónico</label>
        <input type="email" v-model="cita.correo_cliente" class="form-control" placeholder="Correo Electrónico">
      </div>

      <div class="mb-3">
        <label for="telefono" class="form-label">Número de Teléfono</label>
        <input type="tel" v-model="cita.telefono_cliente" class="form-control" placeholder="Número de Teléfono"  required  minlength="8" maxlength="8">
      </div>

      <div class="mb-3">
        <label for="notas" class="form-label">Notas para la cita</label>
        <textarea v-model="cita.notas" class="form-control" rows="3" placeholder="Notas para la cita"></textarea>
      </div>

      <!-- Botón para reservar cita -->
      <button type="submit" class="btn btn-success" :disabled="!horarioSeleccionado || !cita.nombre_cliente || !cita.correo_cliente || !cita.telefono_cliente">Reservar</button>
    </form>

    <!-- Mostrar mensaje solo después de generar la cita exitosamente -->
    <div v-if="mensaje" class="alert alert-info mt-3">
      {{ mensaje }}
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      cita: {
        doctor_id: '',
        nombre_cliente: '',
        correo_cliente: '',
        telefono_cliente: '',
        notas: ''
      },
      doctores: [],
      fechasHorarios: [],  // Aquí almacenaremos la matriz de fechas y horarios
      horarioSeleccionado: null,  // Horario seleccionado para la cita
      mensaje: ''  // Inicialmente vacío
    };
  },
  computed: {
    // Mostrar solo los primeros 7 días si la pantalla es pequeña
    fechasAMostrar() {
      return window.innerWidth < 768 ? this.fechasHorarios.slice(0, 4) : this.fechasHorarios;
    }
  },
  created() {
    this.obtenerDoctores();
    window.addEventListener('resize', this.actualizarFechasAMostrar);
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.actualizarFechasAMostrar);
  },
  methods: {
    actualizarFechasAMostrar() {
      this.$forceUpdate();  // Actualizar cuando se cambie el tamaño de pantalla
    },

    // Obtener doctores
    obtenerDoctores() {
      fetch('https://examencortogrupo4.riegoautomatico.shop/api/public/api.php?action=obtenerDoctores')
        .then(response => response.json())
        .then((data) => {
          this.doctores = data;
        })
        .catch(console.log);
    },

    // Crear la cita
    crearCita() {
      const dataSend = {
        doctor_id: this.cita.doctor_id,
        fecha_cita: this.horarioSeleccionado.fecha,
        hora_inicio: this.horarioSeleccionado.hora_inicio,
        hora_fin: this.horarioSeleccionado.hora_fin,
        nombre_cliente: this.cita.nombre_cliente,
        correo_cliente: this.cita.correo_cliente,
        telefono_cliente: this.cita.telefono_cliente,
        notas: this.cita.notas
      };

      // Realizar la solicitud para crear la cita
      axios
        .post('https://examencortogrupo4.riegoautomatico.shop/api/public/api.php?action=generarCita', dataSend)
        .then(response => {
          // Mostrar mensaje solo si la cita se genera exitosamente
          this.mensaje = 'Cita generada exitosamente', response;
          // Opcionalmente, ocultar el mensaje después de unos segundos
          setTimeout(() => {
            this.mensaje = '';
            window.location.href = "https://citas-veterinarias-grupo4.netlify.app/citas";
          }, 3000);  // El mensaje desaparece después de 5 segundos
        })
        .catch(error => {
          // Mostrar mensaje de error si falla la creación de la cita
          this.mensaje = 'Error al generar la cita';
          console.error('Error al generar la cita:', error);
        });
    },

    // Obtener los horarios de trabajo del doctor
    obtenerHorariosDoctor(doctorId) {
      axios.get(`https://examencortogrupo4.riegoautomatico.shop/api/public/api.php?action=obtenerHorariosTrabajo&doctor_id=${doctorId}`)
        .then(response => {
          const horariosTrabajo = response.data;  // Días y horarios de trabajo
          this.calcularFechasConHorarios(horariosTrabajo);
        })
        .catch(error => {
          console.error('Error obteniendo horarios de trabajo:', error);
        });
    },

    // Calcular las próximas fechas y verificar los horarios ocupados
    calcularFechasConHorarios(horariosTrabajo) {
      const fechas = [];
      const diasTrabajo = horariosTrabajo.map(h => h.dia_semana);
      const hoy = new Date();
      const diasSemana = ['Lunes', 'Martes', 'Miércoles', 'Jueves', 'Viernes', 'Sábado', 'Domingo'];
      const promesas = [];

      for (let i = 0; i < 14; i++) {
        const fecha = new Date(hoy);
        fecha.setDate(hoy.getDate() + i);
        const diaNombre = diasSemana[fecha.getDay() - 1];

        if (diasTrabajo.includes(diaNombre)) {
          const fechaString = fecha.toISOString().split('T')[0];

          // Obtener horarios ocupados para esa fecha
          const promesa = axios.get(`https://examencortogrupo4.riegoautomatico.shop/api/public/api.php?action=obtenerHorariosDoctor&doctor_id=${this.cita.doctor_id}&fecha_cita=${fechaString}`)
            .then(response => {
              const horarios = response.data.horarios.map(horario => ({
                hora_inicio: horario.hora_inicio,
                hora_fin: horario.hora_fin,
                estado: horario.estado
              }));

              fechas.push({ fecha: fechaString, horarios, dia:diaNombre });
            })
            .catch(error => {
              console.error('Error verificando horarios ocupados:', error);
            });

          promesas.push(promesa);
        }
      }

          // Esperar que todas las solicitudes terminen y luego ordenar las fechas
      Promise.all(promesas).then(() => {
        this.fechasHorarios = fechas.sort((a, b) => new Date(a.fecha) - new Date(b.fecha));  // Ordenar fechas
      });
    },

    // Seleccionar un horario, pero no mostrar ningún mensaje
    seleccionarHorario(fecha, horario) {
      this.horarioSeleccionado = {
        fecha: fecha,
        hora_inicio: horario.hora_inicio,
        hora_fin: horario.hora_fin
      };
    }
  }
};
</script>

<style scoped>
/* Estilos para la cuadrícula de horarios */
.horarios-grid {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

@media (max-width: 576px) {
  .horarios-grid button {
    font-size: 14px;
    padding: 8px;
  }
}
</style>
