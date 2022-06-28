<template>
  <section class="src-componentes-formulario">
    <div class="div jumbotron">
      <h2>Componente Formulario</h2>
      <hr />
      <hr />
      <br />

      <vue-form :state="formState" @submit.prevent="addUser()">
        <!-- Campo Nombre -->
        <validate tag="div">
          <!-- Elemento de entrada -->
          <label for="nombre">Nombre</label>
          <input
            type="text"
            id="nombre"
            name="nombre"
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.nombre"
            required
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLength"
            no-espacios
          />
          <!-- Mensajes de validacion -->
          <field-messages name="nombre" show="$dirty">
            <div
              v-if="formState.$dirty"
              slot="required"
              class="alert alert-danger mt-1"
            >
              Campo requerido
            </div>
            <div slot="minlength" class="alert alert-danger mt-1">
              El nombre debe tener entre {{ nombreMinLength }} y
              {{ nombreMaxLength }} caracteres
            </div>
            <div slot="no-espacios" class="alert alert-danger mt-1">
              No se permiten espacios intermedios en este campo.
            </div>
          </field-messages>
        </validate>

        <br />

        <!-- Campo edad -->
        <validate tag="div">
          <!-- Elemento de entrada -->
          <label for="nombre">Edad</label>
          <input
            type="number"
            id="edad"
            name="edad"
            class="form-control"
            autocomplete="off"
            v-model.number="formData.edad"
            required
            :min="edadMin"
            :max="edadMax"
          />
          <!-- Mensajes de validacion -->
          <field-messages name="edad" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="min" class="alert alert-danger mt-1">
              La edad minima permitida es de {{ edadMin }} años.
            </div>
            <div slot="max" class="alert alert-danger mt-1">
              La edad maxima permitida es de {{ edadMax }} años.
            </div>
          </field-messages>
        </validate>

        <br />

        <!-- Campo email -->
        <validate tag="div">
          <!-- Elemento de entrada -->
          <label for="nombre">Email</label>
          <input
            type="email"
            id="email"
            name="email"
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.email"
            required
          />
          <!-- Mensajes de validacion -->
          <field-messages name="email" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="email" class="alert alert-danger mt-1">
              Email no valido
            </div>
          </field-messages>
        </validate>
        <br />

        <!-- Boton envio -->
        <button class="btn btn-success my-4" :disabled="formState.$invalid">
          Agregar Usuario
        </button>
        <hr>
        <button class="btn btn-success my-4" :disabled="formState.$invalid">
          Agregar Usuario Async
        </button>
      </vue-form>
      <!-- <div v-if="users.length" class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Nombre</th>
            <th>Edad</th>
            <th>Email</th>
          </tr>
          <tr v-for="(user, index) in users" :key="index">
            <td>{{ user.nombre }}</td>
            <td>{{ user.edad }}</td>
            <td>{{ user.email }}</td>
          </tr>
        </table>
      </div>
      <h4 v-else class="alert alert-danger text-center">
        No se encontraron usuarios.
      </h4> -->

      <!-- <hr />
      <p><u>formData</u></p>
      <pre>{{ formData }}</pre>

      <hr />
      <p><u>formState</u></p>
      <pre>{{ formState }}</pre> -->
    </div>
  </section>
</template>

<script>
import axios from "axios";

export default {
  name: "src-componentes-formulario",
  props: [],
  mounted() {},
  data() {
    return {
      url: "https://62b8e721ff109cd1dc89476f.mockapi.io/postUsers",
      formState: {},
      formData: this.getInitialData(),
      nombreMinLength: 3,
      nombreMaxLength: 15,
      edadMin: 18,
      edadMax: 120,
      users: [],
    };
  },
  methods: {
    getInitialData() {
      return {
        nombre: "",
        edad: "",
        email: "",
      };
    },
    enviar() {
      this.users.push({ ...this.formData });
      console.log({ ...this.formData });
      this.formData = this.getInitialData(); //Reset de los datos del vue-form
      this.formState._reset(); // reset de los estados del vue-form
    },
    addUser() {
      axios
        .post(this.url, this.formData)
        .then((response) => {
          console.log(response);
        })
        .catch((error) => console.log("error Axios", error));

      this.formData = this.getInitialData();
      this.formState._reset();
    },
    async addUserAsync() {
      try {
        let { resp } = await axios.post(this.url, this.formData);
        console.log(resp.data);
      } catch (err) {
        console.error();
        err;
      }

      this.formData = this.getInitialData();
      this.formState._reset();
    },
  },
  computed: {},
};
</script>

<style scoped lang="css">
.jumbotron {
  background-color: purple;
  color: white;
}

hr {
  background-color: #bbb;
}

pre {
  color: white;
}
</style>
