<template>
  <section class="src-components-usuarios">
    <div class="jumbotro">
      <h1>Usuarios</h1>

      <button class="btn btn-success my-4" @click="getUsuarios()">
          Mostrar Usuarios
        </button>

      <div v-if="users.length" class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Id</th>
            <th>Nombre</th>
            <th>Edad</th>
            <th>Email</th>
          </tr>
          <tr v-for="(user, index) in users" :key="index">
            <td>{{ user.id }}</td>
            <td>{{ user.nombre }}</td>
            <td>{{ user.edad }}</td>
            <td>{{ user.email }}</td>
          </tr>
        </table>
      </div>
      <h4 v-else class="alert alert-danger text-center">
        No se encontraron usuarios.
      </h4>
    </div>
  </section>
</template>

<script>

  export default  {
    name: 'src-components-usuarios',
    props: [],
    mounted () {
    },
    data () {
      return {
        users: [],
        url: "https://62b8e721ff109cd1dc89476f.mockapi.io/postUsers",
      }
    },
    methods: {

     async getUsuarios() {
      try {
        let { data } = await this.axios(this.url);
        this.users = data;
      } catch (error) {
        console.error("Error Axios", error);
      }
      }

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
.src-components-usuarios {
}
</style>
