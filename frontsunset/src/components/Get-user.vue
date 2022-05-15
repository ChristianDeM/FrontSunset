<template>
  <div class="list row">
    <div class="col-md-6">
      <h4> Usuarios </h4>
      <ul class="list-group">
        <li class="list-group-item"
          :class="{ active: index == currentIndex }"
          v-for="(usurios, index) in usurios"
          :key="index"
          @click="setActiveUsuarios(usuarios, index)"
        >
          {{ usurio.Nombre }}
        </li>

      </ul>
    </div>
    <div class="col-md-6">
      <div v-if="currentusuarios">
        <h4>Usuario</h4>
        <div>
          <br><label><strong>Nombre:</strong></label> {{ currentusuarios.Nombre}}

        </div>
        <router-link :to="'/usurio/' + currentusuarios.id" class="btn btn-info"> Editar</router-link>
      </div>
      <div v-else>
        <br />
        <p> Selecciona un explorer.</p>
      </div>
    </div>
  </div>
</template>
<script>

import Usuariosservice from "../services/usuarioservices";

export default {
  name: "user-list",
  data() {
    return {
        Nombre:"",
        Correo:"",
        currentIndex: -1,
    };
  },
  methods: {
    getAllUsuarios(){
      Usuariosservice.getAll()
        .then(response => {
          this.usurios = response.data;
        })
        .catch(e => {
          console.log(e);
        });
    },
    setActiveUsuario(usuarios, index) {
      this.currentusuarios= usuarios;
      this.currentusuarios = usuarios? index : -1;
    }
  },
  mounted() {
    this.getAllUsuarios();
  }
};
</script>