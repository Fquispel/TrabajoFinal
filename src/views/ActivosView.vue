<template>
  <div class="activos">
  </div>
  <h1>Activos Fijos</h1>
  <form @submit.prevent="agregarActivos()">
    <div class="input-group mb-3 justify-content-center">
      <div class="input-group-prepend flex-colunm col-4">
        <select class="form-select" v-model="seleccionarCategoria">
          <option value="undefined" disabled>Seleccione Una Categoria</option>
          <option v-for="selectCategorias in categorias" :key="index">
            {{selectCategorias.nombre}}</option>
        </select>
      </div>
    </div>
    <div class="input-group mb-3 justify-content-center">
      <div class="input-group-prepend flex-colunm col-4">
        <input type="text" class="form-control col-4" placeholder="Marca"
        aria-describedby="button-addon2">
      </div>
    </div>
    <div class="input-group mb-3 justify-content-center">
      <div class="input-group-prepend flex-colunm col-4">
        <input type="text" class="form-control col-4" placeholder="Modelo"
        aria-describedby="button-addon2">
      </div>
    </div>
    <div class="input-group mb-3 justify-content-center">
      <div class="input-group-prepend flex-colunm col-4">
        <select class="form-select">
          <option selected>Seleccione un Estado</option>
          <option>Nuevo</option>
          <option>Usado</option>
          <option>Desuso</option>
        </select>
      </div>
    </div>
    <div class="input-group mb-3 justify-content-center">
      <div class="input-group-prepend flex-colunm col-4">
        <select class="form-select" v-model="seleccionarArea">
          <option value="undefined" disabled>Seleccione Un departamento</option>
          <option v-for="selectArea in area" :key="index">
            {{selectArea.nombreArea}}</option>
        </select>
      </div>
    </div>
    <div class="input-group mb-3 justify-content-center">
      <button class="btn btn-success " type="submit">Agregar</button>
    </div>
  </form>
  <div class="col m12 card-panel">
    <table class="table table-bordered ">
      <thead class="table-dark">
        <tr>
          <th scope="col ">Codigo</th>
          <th scope="col">Categoria</th>
          <th scope="col">Marca</th>
          <th scope="col">Modelo</th>
          <th scope="col">Estado</th>
          <th scope="col">Área</th>
          <th scope="col">Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(activosFijos, index) in activos">
          <th>{{activosFijos.id }}</th>
          <td>{{activosFijos.categoria}}</td>
          <td>{{activosFijos.marca}}</td>
          <td>{{activosFijos.modelo}}</td>
          <td>{{activosFijos.estado}}</td>
          <td>{{activosFijos.area}}</td>
          <td>
            <button @click="formActualizar(index)" class="btn btn-warning">Actualizar</button>
            <button @click="borrarCategoria(index)" class="btn btn-danger">Borrar</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
    export default {
        name: 'activosView',
        data(){
            return {
                activosReg:{

                },
                categorias:[],
                area:[],
                activos:[]
            }
        },
        methods: {
            agregarActivos(){
                axios({
                    method: "post",
                    url: "http://localhost:3000/activos",
                    data: this.activosReg
                })
                .then(response => {
                    console.log(response);
                })
                .catch(e => console.log(e));
            },
            getActivosFijos(){
                axios({
                    method: "get",
                    url: "http://localhost:3000/activos"
                })
                .then(response => {
                    this.activos = response.data;
                console.log(response);
                })
                .catch(e => console.log(e));
            },
            getCategorias(){
              axios({
                method: "get",
                url: "http://localhost:3000/categorias",
              })
              .then(response => {
                this.categorias = response.data;
                console.log(response);
              })
              .catch(e => console.log(e));
            },
            getArea(){
                axios({
                    method: "get",
                    url: "http://localhost:3000/area"
                })
                .then(response => {
                    this.area = response.data;
                console.log(response);
                })
                .catch(e => console.log(e));
            },
        },
        computed: {
        },
        mounted(){
            this.getActivosFijos()
            this.getCategorias()
            this.getArea()
        },
        components: {
        }
    }
</script>
<style>

</style>
