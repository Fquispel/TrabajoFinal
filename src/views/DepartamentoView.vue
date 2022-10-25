<template>
  <div class="departamento">
    <h1>Departamentos</h1>
  </div>
  <form @submit.prevent="agregarArea()">
    <div class="input-group mb-3 justify-content-center">
      <div class="input-group-prepend flex-colunm col-4">
        <input type="text" class="form-control col-4" v-model="areaReg.nombreArea" placeholder="Area" required
        aria-describedby="button-addon2">
      </div>
    </div>
    <div class="input-group mb-3 justify-content-center">
      <div class="input-group-prepend flex-colunm col-4">
        <input type="text" class="form-control col-4" v-model="areaReg.nombreEncargado" placeholder=" Nombre del Encargado" required
        aria-describedby="button-addon2">
      </div>
    </div>
    <div class="input-group mb-3 justify-content-center">
      <div class="input-group-prepend flex-colunm col-4">
        <input type="text" class="form-control col-4" v-model="areaReg.numeroFuncionarios" placeholder="Numero de Funcionarios" required
        aria-describedby="button-addon2">
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
          <th scope="col">Codigo</th>
          <th scope="col">Area</th>
          <th scope="col">Nombre Encargado</th>
          <th scope="col">Numero de Funcionarios</th>
          <th scope="col">Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(departamento, index) in area">
          <th>{{ departamento.id }}</th>
          <td>{{ departamento.nombreArea}}</td>
          <td>{{ departamento.nombreEncargado}}</td>
          <td>{{ departamento.numeroFuncionarios}}</td>
          <td>
            <button @click="actualizarArea(departamento.id)" class="btn btn-warning">Actualizar</button>
            <button @click="borrarArea(departamento.id)" class="btn btn-danger">Borrar</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
    export default {
        name: 'departamentoView',
        data(){
            return {
                areaReg:{
                  nombreArea:null,
                  nombreEncargado:null,
                  numeroFuncionarios:null
                },
                area:[]
            }
        },
        methods: {
            agregarArea(){
                axios({
                    method: "post",
                    url: "http://localhost:3000/area",
                    data: this.areaReg
                })
                .then(response => {
                    console.log(response);
                    this.getArea()
                })
                .catch(e => console.log(e));
            },
            borrarArea(area_id){
              if (confirm("Está seguro de eliminar el Departamento " + area_id + "?"))
                axios({
                    method: "delete",
                    url: "http://localhost:3000/area/"+area_id,
                    data: this.area
                })
                .then(response => {
                    console.log(response);
                    this.getArea()
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
            this.getArea()
        },
        components: {
        }
    }
</script>
<style>

</style>
